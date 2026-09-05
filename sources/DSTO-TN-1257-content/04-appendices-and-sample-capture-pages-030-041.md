# Appendices and sample capture

Source: `DSTO-TN-1257.pdf`, PDF pages 30-41.

Navigation: previous [Testing and conclusions](03-testing-and-conclusions-pages-025-029.md) | [coverage index](README.md) | next none

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-30"></a>

## Source PDF page 30

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

22 { -        offset = parseFields(tvb, tree, offset, paramParser); +        offset = parseFields(tvb, tree, offset, paramParser, pinfo); }

/* Should alignment padding be added */ @@ -1105,7 +1126,7 @@ gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset) /* Parse a variable electromagnetic emission system beam. */ gint parseField_ElectromagneticEmissionSystemBeam( -    tvbuff_t *tvb, proto_tree *tree, gint offset) +    tvbuff_t *tvb, proto_tree *tree, gint offset, packet_info *pinfo) { DIS_ParserNode *paramParser = 0;

@@ -1116,7 +1137,7 @@ gint parseField_ElectromagneticEmissionSystemBeam( /* Parse the variable parameter fields */ if (paramParser) { -        offset = parseFields(tvb, tree, offset, paramParser); +        offset = parseFields(tvb, tree, offset, paramParser, pinfo); }

return offset; diff --git a/epan/dissectors/packet-dis-fields.h b/epan/dissectors/packet-dis-fields.h index d306a4d..477bcdb 100644 --- a/epan/dissectors/packet-dis-fields.h +++ b/epan/dissectors/packet-dis-fields.h @@ -54,6 +54,7 @@ extern int hf_dis_radio_id; extern int hf_dis_ens; extern int hf_dis_ens_class; extern int hf_dis_ens_type; +extern int hf_dis_ens_type_audio; extern int hf_dis_tdl_type; extern int hf_dis_sample_rate; extern int hf_dis_data_length; @@ -96,9 +97,17 @@ extern int hf_dis_antenna_pattern_parameter_dump; extern int hf_dis_num_shafts; extern int hf_dis_num_apas; extern int hf_dis_num_ua_emitter_systems; +extern int hf_dis_signal_link16_npg; +extern int hf_dis_signal_link16_tsec_cvll; +extern int hf_dis_signal_link16_msec_cvll; +extern int hf_dis_signal_link16_message_type; +extern int hf_dis_signal_link16_ptt; +extern int hf_dis_signal_link16_stn;

extern int ett_dis_ens; extern int ett_dis_crypto_key; +extern int ett_dis_signal_link16_network_header; +extern int ett_dis_signal_link16_message_data;

@@ -214,6 +223,10 @@ typedef enum

### DIS_FIELDTYPE_TRANSMITTER_SECONDARY_MODE,

### DIS_FIELDTYPE_JTIDS_SYNC_STATE,

### DIS_FIELDTYPE_NETWORK_SYNC_ID,

### +    DIS_FIELDTYPE_LINK16_NPG,

### +    DIS_FIELDTYPE_LINK16_TSEC_CVLL,

### +    DIS_FIELDTYPE_LINK16_MSEC_CVLL,

### +    DIS_FIELDTYPE_LINK16_MESSAGE_TYPE,

### DIS_FIELDTYPE_NUM_ELECTROMAGNETIC_EMISSION_SYSTEMS,

### DIS_FIELDTYPE_NUM_OF_SHAFTS,

### DIS_FIELDTYPE_NUM_OF_APAS,

@@ -244,6 +257,8 @@ typedef enum

### DIS_FIELDTYPE_ANTENNA_PATTERN_PARAMETERS,

### DIS_FIELDTYPE_MOD_PARAMS_CCTT_SINCGARS,

### DIS_FIELDTYPE_MOD_PARAMS_JTIDS_MIDS,

### +    DIS_FIELDTYPE_LINK16_MESSAGE_DATA,

<a id="source-pdf-page-31"></a>

## Source PDF page 31

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

23

### +    DIS_FIELDTYPE_LINK16_PTT,

### DIS_FIELDTYPE_ELECTROMAGNETIC_EMISSION_SYSTEM_BEAM,

### DIS_FIELDTYPE_ELECTROMAGNETIC_EMISSION_SYSTEM,

### DIS_FIELDTYPE_EMITTER_SYSTEM,

@@ -316,6 +331,7 @@ extern DIS_ParserNode DIS_FIELDS_VECTOR_FLOAT_32[]; extern DIS_ParserNode DIS_FIELDS_VECTOR_FLOAT_64[]; extern DIS_ParserNode DIS_FIELDS_MOD_PARAMS_CCTT_SINCGARS[]; extern DIS_ParserNode DIS_FIELDS_MOD_PARAMS_JTIDS_MIDS[]; +extern DIS_ParserNode DIS_FIELDS_SIGNAL_LINK16_NETWORK_HEADER[]; extern DIS_ParserNode DIS_FIELDS_EMITTER_SYSTEM[]; extern DIS_ParserNode DIS_FIELDS_FUNDAMENTAL_PARAMETER_DATA[]; extern DIS_ParserNode DIS_FIELDS_TRACK_JAM[]; @@ -360,11 +376,11 @@ extern gint parseField_Double(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_

extern gint parseField_Timestamp(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode parserNode);

-extern gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree, gint offset); +extern gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree, gint offset, packet_info *pinfo);

-extern gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset); +extern gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset, packet_info *pinfo);

-extern gint parseField_ElectromagneticEmissionSystemBeam(tvbuff_t *tvb, proto_tree *tree, gint offset); +extern gint parseField_ElectromagneticEmissionSystemBeam(tvbuff_t *tvb, proto_tree *tree, gint offset, packet_info *pinfo);

extern guint32 disProtocolVersion; extern guint32 pduType; @@ -375,7 +391,9 @@ extern guint32 entityDomain; extern guint32 radioID; extern guint32 disRadioTransmitState; extern guint32 encodingScheme; +extern guint32 tdlType; extern guint32 numSamples; +extern guint32 messageType; extern guint32 numFixed; extern guint32 numVariable; extern guint32 numBeams; diff --git a/epan/dissectors/packet-dis-pdus.c b/epan/dissectors/packet-dis-pdus.c index 939c759..f1e1f30 100644 --- a/epan/dissectors/packet-dis-pdus.c +++ b/epan/dissectors/packet-dis-pdus.c @@ -29,6 +29,8 @@ #include "packet-dis-pdus.h" #include "packet-dis-fields.h" #include "packet-dis-enums.h" +#include "packet-link16.h" +#include "packet-ntp.h"

#define DIS_PDU_MAX_VARIABLE_PARAMETERS              16 #define DIS_PDU_MAX_VARIABLE_RECORDS                 16 @@ -131,7 +133,7 @@ DIS_ParserNode DIS_PARSER_SIGNAL_PDU[] = { DIS_FIELDTYPE_ENTITY_ID,               "Entity ID",0,0,0,0 }, { DIS_FIELDTYPE_RADIO_ID,                "Radio ID",0,0,0,&radioID }, { DIS_FIELDTYPE_ENCODING_SCHEME,         "Encoding Scheme",0,0,0,&encodingScheme }, -    { DIS_FIELDTYPE_TDL_TYPE,                "TDL Type",0,0,0,0 }, +    { DIS_FIELDTYPE_TDL_TYPE,                "TDL Type",0,0,0,&tdlType }, { DIS_FIELDTYPE_SAMPLE_RATE,             "Sample Rate",0,0,0,0 }, { DIS_FIELDTYPE_DATA_LENGTH,             "Data Length",0,0,0,0 }, { DIS_FIELDTYPE_NUMBER_OF_SAMPLES,       "Number of Samples",0,0,0,&numSamples }, @@ -732,9 +734,92 @@ void initializeParser(DIS_ParserNode parserNodes[]) } }

+/* Parse Link 16 Message Data record (SISO-STD-002, Tables 5.2.5 through 5.2.12) + */

<a id="source-pdf-page-32"></a>

## Source PDF page 32

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

24 +static gint parse_Link16_Message_Data(proto_tree *tree, tvbuff_t *tvb, gint offset, packet_info *pinfo) +{ +    guint32 cache, value, i; +    Link16State state; +    tvbuff_t *newtvb; + +    switch (messageType) { +    case DIS_MESSAGE_TYPE_JTIDS_HEADER_MESSAGES: +        cache = tvb_get_ntohl(tvb, offset); +        value = cache & 0x7; +        proto_tree_add_text(tree, tvb, offset, 4, +            "Time Slot Type: %d", value); + +        value = (cache >> 3) & 0x1; +        proto_tree_add_text(tree, tvb, offset, 4, +            "Relay Transmission Indicator: %d", value); + +        value = (cache >> 4) & 0x7FFF; +        proto_tree_add_uint(tree, hf_dis_signal_link16_stn, tvb, offset, 4, value); + +        col_append_fstr(pinfo->cinfo, COL_INFO, ", STN=0%o, Link 16 Words:", value); + +        value = (cache >> 19); +        offset += 4; + +        cache = tvb_get_ntohl(tvb, offset); +        value |= (cache & 0x7) << 13; +        proto_tree_add_text(tree, tvb, offset - 4, 8, +            "Secure Data Unit Serial Number: %d", value); + +        offset += 4; + +        memset(&state, 0, sizeof(state)); +        pinfo->private_data = &state; + +        for (i = 0; i < (encodingScheme & 0x3FFF); i++) { +            gint8 *word = (gint8 *)g_malloc(10); +            if (!(i & 1)) { +                word[0] = (cache >> 16) & 0xFF; +                word[1] = (cache >> 24) & 0xFF; +                cache = tvb_get_ntohl(tvb, offset); +                offset += 4; +                word[2] = cache & 0xFF; +                word[3] = (cache >> 8) & 0xFF; +                word[4] = (cache >> 16) & 0xFF; +                word[5] = (cache >> 24) & 0xFF; +                cache = tvb_get_ntohl(tvb, offset); +                offset += 4; +                word[6] = cache & 0xFF; +                word[7] = (cache >> 8) & 0xFF; +                word[8] = (cache >> 16) & 0xFF; +                word[9] = (cache >> 24) & 0xFF; +            } else { +                cache = tvb_get_ntohl(tvb, offset); +                offset += 4; +                word[0] = cache & 0xFF; +                word[1] = (cache >> 8) & 0xFF; +                word[2] = (cache >> 16) & 0xFF; +                word[3] = (cache >> 24) & 0xFF; +                cache = tvb_get_ntohl(tvb, offset); +                offset += 4; +                word[4] = cache & 0xFF; +                word[5] = (cache >> 8) & 0xFF; +                word[6] = (cache >> 16) & 0xFF; +                word[7] = (cache >> 24) & 0xFF; +                cache = tvb_get_ntohl(tvb, offset); +                offset += 4; +                word[8] = cache & 0xFF; +                word[9] = (cache >> 8) & 0xFF; +            }

<a id="source-pdf-page-33"></a>

## Source PDF page 33

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

25 + +            newtvb = tvb_new_child_real_data(tvb, word, 10, 10); +            tvb_set_free_cb(newtvb, g_free); +            add_new_data_source(pinfo, newtvb, "Link 16 Word"); +            call_dissector(find_dissector("link16"), newtvb, pinfo, tree); +        } +        break; +    } +    return offset; +} + /* Parse packet data based on a specified array of DIS_ParserNodes. */ -gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode parserNodes[]) +gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode parserNodes[], packet_info *pinfo) { guint        fieldIndex     = 0; guint        fieldRepeatLen = 0; @@ -839,13 +924,17 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa pi = proto_tree_add_item(tree, hf_dis_ens, tvb, offset, 2, ENC_BIG_ENDIAN); sub_tree = proto_item_add_subtree(pi, ett_dis_ens); proto_tree_add_item(sub_tree, hf_dis_ens_class, tvb, offset, 2,

### ENC_BIG_ENDIAN);

-            proto_tree_add_item(sub_tree, hf_dis_ens_type, tvb, offset, 2, ENC_BIG_ENDIAN);

+            proto_tree_add_item(sub_tree, +                (uintVal >> 14) == DIS_ENCODING_CLASS_ENCODED_AUDIO ? hf_dis_ens_type_audio : hf_dis_ens_type, +                tvb, offset, 2, ENC_BIG_ENDIAN); proto_item_set_end(pi, tvb, offset); *(parserNodes[fieldIndex].outputVar) = (guint32)uintVal; offset += 2; break; case DIS_FIELDTYPE_TDL_TYPE: +            uintVal = tvb_get_ntohs(tvb, offset); proto_tree_add_item(tree, hf_dis_tdl_type, tvb, offset, 2, ENC_BIG_ENDIAN); +            *(parserNodes[fieldIndex].outputVar) = (guint32)uintVal; offset += 2; break; case DIS_FIELDTYPE_SAMPLE_RATE: @@ -862,12 +951,31 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa *(parserNodes[fieldIndex].outputVar) = (guint32)uintVal; offset += 2; break; case DIS_FIELDTYPE_RADIO_DATA: -            newtvb = tvb_new_subset_remaining(tvb, offset); -            proto_tree_add_item(tree, hf_dis_signal_data, newtvb, 0, -1, ENC_NA ); +            if (tdlType == DIS_TDL_TYPE_LINK16_STD) { +                pi = proto_tree_add_text(tree, tvb, offset, 16, "Link 16 Network Header"); +                sub_tree = proto_item_add_subtree(pi, ett_dis_signal_link16_network_header); +                offset = parseFields(tvb, sub_tree, offset, DIS_FIELDS_SIGNAL_LINK16_NETWORK_HEADER, pinfo); +                proto_item_set_end(pi, tvb, offset); + +                pi = proto_tree_add_text(tree, tvb, offset, -1, "Link 16 Message Data: %s",

+                    val_to_str(messageType, DIS_PDU_Link16_MessageType_Strings, "")); +                sub_tree = proto_item_add_subtree(pi, ett_dis_signal_link16_message_data); +                offset = parse_Link16_Message_Data(sub_tree, tvb, offset, pinfo); +                proto_item_set_end(pi, tvb, offset); +            } else { +                newtvb = tvb_new_subset_remaining(tvb, offset); +                proto_tree_add_item(tree, hf_dis_signal_data, newtvb, 0, -1, ENC_NA ); +            } /* ****ck******* need to look for padding bytes */ break; +        case DIS_FIELDTYPE_LINK16_PTT:

<a id="source-pdf-page-34"></a>

## Source PDF page 34

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

26 +            if (tvb_get_ntohl(tvb, offset) == 0xFFFFFFFF) +                proto_tree_add_text(tree, tvb, offset, 8, "%s: NO STATEMENT", parserNodes[fieldIndex].fieldLabel); +            else +                proto_tree_add_item(tree, hf_dis_signal_link16_ptt, tvb, offset, 8,

### ENC_TIME_NTP|ENC_BIG_ENDIAN);

+            offset += 8; +            break; case DIS_FIELDTYPE_RADIO_CATEGORY: proto_tree_add_item(tree, hf_dis_radio_category, tvb, offset, 1,

### ENC_BIG_ENDIAN);

offset += 1; @@ -1003,7 +1111,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa pi = proto_tree_add_text(tree, tvb, offset, -1, "%s", parserNodes[fieldIndex].fieldLabel); sub_tree = proto_item_add_subtree(pi, parserNodes[fieldIndex].ettVar); -                    offset = parseFields(tvb, sub_tree, offset,

### DIS_FIELDS_MOD_PARAMS_CCTT_SINCGARS);

+                    offset = parseFields(tvb, sub_tree, offset, DIS_FIELDS_MOD_PARAMS_CCTT_SINCGARS, pinfo); proto_item_set_end(pi, tvb, offset); break; } @@ -1011,7 +1119,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa pi = proto_tree_add_text(tree, tvb, offset, -1, "%s", parserNodes[fieldIndex].fieldLabel); sub_tree = proto_item_add_subtree(pi, parserNodes[fieldIndex].ettVar); -                    offset = parseFields(tvb, sub_tree, offset,

### DIS_FIELDS_MOD_PARAMS_JTIDS_MIDS);

+                    offset = parseFields(tvb, sub_tree, offset, DIS_FIELDS_MOD_PARAMS_JTIDS_MIDS, pinfo); proto_item_set_end(pi, tvb, offset); break; } @@ -1028,7 +1136,18 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa newtvb = tvb_new_subset_remaining(tvb, offset); proto_tree_add_item(tree, hf_dis_antenna_pattern_parameter_dump, newtvb, 0, - 1,

### ENC_NA );

break; - +        case DIS_FIELDTYPE_LINK16_NPG: +            proto_tree_add_item(tree, hf_dis_signal_link16_npg, tvb, offset, 2,

### ENC_BIG_ENDIAN);

+            offset += 2; +            break; +        case DIS_FIELDTYPE_LINK16_TSEC_CVLL: +            proto_tree_add_item(tree, hf_dis_signal_link16_tsec_cvll, tvb, offset, 1,

### ENC_NA);

+            offset++; +            break; +        case DIS_FIELDTYPE_LINK16_MSEC_CVLL: +            proto_tree_add_item(tree, hf_dis_signal_link16_msec_cvll, tvb, offset, 1,

### ENC_NA);

+            offset++; +            break;

/* padding */ case DIS_FIELDTYPE_PAD8: @@ -1066,6 +1185,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa case DIS_FIELDTYPE_PERSISTENT_OBJECT_TYPE: case DIS_FIELDTYPE_EMISSION_FUNCTION: case DIS_FIELDTYPE_BEAM_FUNCTION: +        case DIS_FIELDTYPE_LINK16_MESSAGE_TYPE: offset = parseField_Enum(tvb, tree, offset, parserNodes[fieldIndex], 1); break; @@ -1210,7 +1330,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset,

<a id="source-pdf-page-35"></a>

## Source PDF page 35

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

27 DIS_ParserNode pa proto_item *newSubtree = proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                    parserNodes[fieldIndex].children); +                    parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); break; @@ -1248,7 +1368,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa parserNodes[fieldIndex].fieldLabel); newSubtree = proto_item_add_subtree(newField, ettFixedData); offset = parseFields (tvb, newSubtree, offset, -                         parserNodes[fieldIndex].children); +                         parserNodes[fieldIndex].children, pinfo); proto_item_set_end(newField, tvb, offset); } } @@ -1274,7 +1394,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa /* XXX is this really necessary? */ tvb_ensure_length_remaining(tvb, offset+4); offset = parseFields (tvb, newSubtree, offset, -                        parserNodes[fieldIndex].children); +                        parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1296,7 +1416,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa (newField, ettVariableData); offset = parseFields (tvb, newSubtree, offset, -                         parserNodes[fieldIndex].children); +                         parserNodes[fieldIndex].children, pinfo); proto_item_set_end(newField, tvb, offset); }

@@ -1321,7 +1441,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa { offset = parseFields (tvb, newSubtree, offset, -                         parserNodes[fieldIndex].children); +                         parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1344,9 +1464,9 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa ettVariableParameters[i]); offset = parseFields (tvb, newSubtree, offset, -                         parserNodes[fieldIndex].children); +                         parserNodes[fieldIndex].children, pinfo); offset = parseField_VariableParameter -                        (tvb, newSubtree, offset); +                        (tvb, newSubtree, offset, pinfo); proto_item_set_end(newField, tvb, offset); } } @@ -1369,9 +1489,9 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa ettVariableRecords[i]); offset = parseFields (tvb, newSubtree, offset, -                         parserNodes[fieldIndex].children); +                         parserNodes[fieldIndex].children, pinfo); offset = parseField_VariableRecord -                        (tvb, newSubtree, offset);

<a id="source-pdf-page-36"></a>

## Source PDF page 36

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

28 +                        (tvb, newSubtree, offset, pinfo); proto_item_set_end(newField, tvb, offset); } } @@ -1390,7 +1510,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1410,7 +1530,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1441,7 +1561,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1474,7 +1594,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1507,7 +1627,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1547,7 +1667,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo); } proto_item_set_end(newField, tvb, offset); } @@ -1572,7 +1692,7 @@ gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode pa proto_item_add_subtree(newField, parserNodes[fieldIndex].ettVar); offset = parseFields(tvb, newSubtree, offset, -                            parserNodes[fieldIndex].children); +                            parserNodes[fieldIndex].children, pinfo);

<a id="source-pdf-page-37"></a>

## Source PDF page 37

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

29 } proto_item_set_end(newField, tvb, offset); } diff --git a/epan/dissectors/packet-dis-pdus.h b/epan/dissectors/packet-dis-pdus.h index e964371..b9d2448 100644 --- a/epan/dissectors/packet-dis-pdus.h +++ b/epan/dissectors/packet-dis-pdus.h @@ -111,6 +111,6 @@ void initializeParser(DIS_ParserNode parserNodes[]);

void initializeParsers(void);

-gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode parserNodes[]); +gint parseFields(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNode parserNodes[], packet_info *pinfo);

#endif /* packet-dis-pduparsers.h */ diff --git a/epan/dissectors/packet-dis.c b/epan/dissectors/packet-dis.c index da012a9..0a00009 100644 --- a/epan/dissectors/packet-dis.c +++ b/epan/dissectors/packet-dis.c @@ -46,6 +46,7 @@ #include "packet-dis-enums.h" #include "packet-dis-pdus.h" #include "packet-dis-fields.h" +#include "packet-link16.h"

#define DEFAULT_DIS_UDP_PORT 3000

@@ -80,6 +81,7 @@ int hf_dis_radio_id = -1; int hf_dis_ens = -1; int hf_dis_ens_class = -1; int hf_dis_ens_type = -1; +int hf_dis_ens_type_audio = -1; int hf_dis_tdl_type = -1; int hf_dis_sample_rate = -1; int hf_dis_data_length = -1; @@ -122,6 +124,12 @@ int hf_dis_antenna_pattern_parameter_dump = -1; int hf_dis_num_shafts = -1; int hf_dis_num_apas = -1; int hf_dis_num_ua_emitter_systems = -1; +int hf_dis_signal_link16_npg = -1; +int hf_dis_signal_link16_tsec_cvll = -1; +int hf_dis_signal_link16_msec_cvll = -1; +int hf_dis_signal_link16_message_type = -1; +int hf_dis_signal_link16_ptt = -1; +int hf_dis_signal_link16_stn = -1;

/* Initialize the subtree pointers */ static gint ett_dis = -1; @@ -130,6 +138,8 @@ static gint ett_dis_po_header = -1; static gint ett_dis_payload = -1; int ett_dis_ens = -1; int ett_dis_crypto_key = -1; +int ett_dis_signal_link16_network_header = -1; +int ett_dis_signal_link16_message_data = -1;

static const true_false_string dis_modulation_spread_spectrum = { "Spread Spectrum modulation in use", @@ -206,7 +216,7 @@ static gint dissect_dis(tvbuff_t *tvb, packet_info *pinfo, proto_tree *tree, voi */ dis_header_node = proto_tree_add_text(dis_tree, tvb, offset, -1, "Header"); dis_header_tree = proto_item_add_subtree(dis_header_node, ett_dis_header); -    offset = parseFields(tvb, dis_header_tree, offset, DIS_FIELDS_PDU_HEADER); +    offset = parseFields(tvb, dis_header_tree, offset, DIS_FIELDS_PDU_HEADER, pinfo);

proto_item_set_end(dis_header_node, tvb, offset);

@@ -230,7 +240,7 @@ static gint dissect_dis(tvbuff_t *tvb, packet_info *pinfo, proto_tree *tree, voi

<a id="source-pdf-page-38"></a>

## Source PDF page 38

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

30 (dis_po_header_node, ett_dis_po_header); offset = parseFields (tvb, dis_po_header_tree, offset,

### -                 DIS_FIELDS_PERSISTENT_OBJECT_HEADER);

+                 DIS_FIELDS_PERSISTENT_OBJECT_HEADER, pinfo); proto_item_set_end(dis_po_header_node, tvb, offset);

/* Locate the appropriate PO PDU parser, if type is known. @@ -400,13 +410,15 @@ static gint dissect_dis(tvbuff_t *tvb, packet_info *pinfo, proto_tree *tree, voi break; }

+    col_clear(pinfo->cinfo, COL_INFO); + /* If a parser was located, invoke it on the data packet. */ if (pduParser != 0) { dis_payload_tree = proto_item_add_subtree(dis_payload_node, ett_dis_payload); -        offset = parseFields(tvb, dis_payload_tree, offset, pduParser); +        offset = parseFields(tvb, dis_payload_tree, offset, pduParser, pinfo);

proto_item_set_end(dis_payload_node, tvb, offset); } @@ -434,13 +446,17 @@ static gint dissect_dis(tvbuff_t *tvb, packet_info *pinfo, proto_tree *tree, voi ); break; case DIS_PDUTYPE_SIGNAL: -        col_add_fstr( pinfo->cinfo, COL_INFO, -                      "PDUType: %s, RadioID=%u, Encoding Type=%s, Number of Samples=%u", -                      pduString, -                      radioID, -                      val_to_str_const(DIS_ENCODING_TYPE(encodingScheme), DIS_PDU_Encoding_Type_Strings, "Unknown Encoding Type"), -                      numSamples -                      ); +        if (numSamples) +            col_prepend_fstr(pinfo->cinfo, COL_INFO, ", Number of Samples=%u", +                numSamples); + +        if ((encodingScheme & 0xC000) >> 14 == DIS_ENCODING_CLASS_ENCODED_AUDIO) +            col_prepend_fstr(pinfo->cinfo, COL_INFO,", Encoding Type=%s", +                val_to_str_const(DIS_ENCODING_TYPE(encodingScheme), +                DIS_PDU_Encoding_Type_Strings, "Unknown")); + +        col_prepend_fstr( pinfo->cinfo, COL_INFO, +                      "PDUType: %s, RadioID=%u", pduString, radioID); break; case DIS_PDUTYPE_TRANSMITTER: col_add_fstr( pinfo->cinfo, COL_INFO, @@ -593,6 +609,11 @@ void proto_register_dis(void) }, { &hf_dis_ens_type, { "Encoding Type", "dis.radio.encoding_type", +                FT_UINT16, BASE_DEC, NULL, 0x3fff,

### +                NULL, HFILL }

+            }, +            { &hf_dis_ens_type_audio, +              { "Encoding Type",  "dis.radio.encoding_type.audio", FT_UINT16, BASE_DEC, VALS(DIS_PDU_Encoding_Type_Strings), 0x3fff,

### NULL, HFILL }

}, @@ -791,6 +812,35 @@ void proto_register_dis(void) FT_BYTES, BASE_NONE, NULL, 0x0,

### NULL, HFILL}

}, +            { &hf_dis_signal_link16_npg, +              { "NPG Number", "dis.signal.link16.npg",

<a id="source-pdf-page-39"></a>

## Source PDF page 39

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

31 +                 FT_UINT16, BASE_DEC, VALS(Link16_NPG_Strings), 0x0,

### +                 NULL, HFILL }

+            }, +            { &hf_dis_signal_link16_tsec_cvll, +              { "TSEC CVLL", "dis.signal.link16.tsec_cvll",

### +                 FT_UINT8, BASE_RANGE_STRING | BASE_DEC,

RVALS(DIS_PDU_Link16_CVLL_Strings), 0x0,

### +                 NULL, HFILL }

+            }, +            { &hf_dis_signal_link16_msec_cvll, +              { "MSEC CVLL", "dis.signal.link16.msec_cvll",

### +                 FT_UINT8, BASE_RANGE_STRING | BASE_DEC,

RVALS(DIS_PDU_Link16_CVLL_Strings), 0x0,

### +                 NULL, HFILL }

+            }, +            { &hf_dis_signal_link16_message_type, +              { "Message Type", "dis.signal.link16.message_type", +                 FT_UINT8, BASE_DEC, VALS(DIS_PDU_Link16_MessageType_Strings), 0x0,

### +                 NULL, HFILL }

+            }, +            { &hf_dis_signal_link16_ptt, +              { "Perceived Transmit Time", "dis.signal.link16.ptt", +                FT_ABSOLUTE_TIME, ABSOLUTE_TIME_UTC, NULL, 0x0,

### +                NULL, HFILL }

+            }, +            { &hf_dis_signal_link16_stn, +              { "Source Track Number", "dis.signal.link16.stn", FT_UINT16, BASE_OCT, NULL, 0x0,

### +                 NULL, HFILL }

+            }, { &hf_dis_num_shafts, { "Number of Shafts",  "dis.ua.number_of_shafts", FT_UINT8, BASE_DEC, NULL, 0x0, @@ -816,7 +866,9 @@ void proto_register_dis(void) &ett_dis_po_header, &ett_dis_ens, &ett_dis_crypto_key, -        &ett_dis_payload +        &ett_dis_payload, +        &ett_dis_signal_link16_network_header, +        &ett_dis_signal_link16_message_data, };

module_t *dis_module; -- 1.8.1.2

### Figure A2: Software patch (part 2 of 3)

From 6ef9c448729ba0270a4f2552b817d1ceb4fc4de7 Mon Sep 17 00:00:00 2001 From: Peter Ross <peter.ross@dsto.defence.gov.au> Date: Wed, 16 Oct 2013 10:00:03 +1100 Subject: [PATCH 3/3] packet-dis: correct 'Terminal Primary Mode' and 'Sync State' enumeration values

SISO-STD-002 Standard for Link 16 Simulations, June 2006: http://www.sisostds.org/DigitalLibrary.aspx?Command=Core_Download&EntryId=30265 --epan/dissectors/packet-dis-enums.c | 9 ++++-----

### 1 file changed, 4 insertions(+), 5 deletions(-)

diff --git a/epan/dissectors/packet-dis-enums.c b/epan/dissectors/packet-dis-enums.c index d53b3a7..835bb17 100644 --- a/epan/dissectors/packet-dis-enums.c +++ b/epan/dissectors/packet-dis-enums.c @@ -668,8 +668,8 @@ const value_string DIS_PDU_TSAllocationFidelity_Strings[] =

const value_string DIS_PDU_TerminalPrimaryMode_Strings[] = {

<a id="source-pdf-page-40"></a>

## Source PDF page 40

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

32

### -    {0,    "NTR" },

-    {1,    "JTIDS Unit Participant" },

### +    {1,    "NTR" },

+    {2,    "JTIDS Unit Participant" },

### {0,    NULL }

};

@@ -685,9 +685,8 @@ const value_string DIS_PDU_TerminalSecondaryMode_Strings[] = /* http://discussions.sisostds.org/threadview.aspx?fid=18&threadid=53172 */ const value_string DIS_PDU_ModParamSyncState_Strings[] = { -    {0,    "Undefined" }, -    {1,    "Coarse Synchronization" }, -    {1,    "Fine Synchronization" }, +    {2,    "Coarse Synchronization" }, +    {3,    "Fine Synchronization" },

### {0,    NULL }

};

-- 1.8.1.2

### Figure A3: Software patch (part 3 of 3)

<a id="source-pdf-page-41"></a>

## Source PDF page 41

Page classification:  UNCLASSIFIED

### DEFENCE SCIENCE AND TECHNOLOGY ORGANISATION

### DOCUMENT CONTROL DATA 1.  PRIVACY MARKING/CAVEAT (OF DOCUMENT)

### 2.  TITLE

Extending the Wireshark Network Protocol Analyser to Decode Link 16 Tactical Data Link Messages

### 3.  SECURITY CLASSIFICATION (FOR UNCLASSIFIED REPORTS

### THAT ARE LIMITED RELEASE USE (L)  NEXT TO DOCUMENT

### CLASSIFICATION)

Document   (U) Title   (U) Abstract    (U)

### 4.  AUTHOR(S)

William Robertson and Peter Ross

### 5.  CORPORATE AUTHOR

DSTO Defence Science and Technology Organisation

### 506 Lorimer St

Fishermans Bend Victoria 3207 Australia

6a. DSTO NUMBER

### DSTO-TN-1257

6b. AR NUMBER

### AR-015-847

6c. TYPE OF REPORT Technical Note

### 7.  DOCUMENT  DATE

January 2014

### 8.  FILE NUMBER

2013/1123978/1

### 9.  TASK NUMBER

### N/A

### 10.  TASK SPONSOR

### CAD

### 11. NO. OF PAGES

32

### 12. NO. OF REFERENCES

20 13. URL on the World Wide Web

http://dspace.dsto.defence.gov.au/dspace/

### 14. RELEASE AUTHORITY

Chief, Aerospace Division

### 15. SECONDARY RELEASE STATEMENT OF THIS DOCUMENT

Approved for public release

### OVERSEAS ENQUIRIES OUTSIDE STATED LIMITATIONS SHOULD BE REFERRED THROUGH DOCUMENT EXCHANGE, PO BOX 1500, EDINBURGH, SA 5111

### 16. DELIBERATE ANNOUNCEMENT

No Limitations

17.  CITATION IN OTHER DOCUMENTS        Yes 18. DSTO RESEARCH LIBRARY THESAURUS  http://web-vic.dsto.defence.gov.au/workareas/library/resources/dsto_thesaurus.shtml

Network analysis, Network protocols, Simulation, Software tools, Tactical data links, Testing.

### 19. ABSTRACT

This technical note describes the development of a tactical data link message dissector for the Wireshark network protocol analyser. Link 16 is a United States and North Atlantic Treaty Organization standard for secure real-time exchange of tactical information between warfighting units. Concurrent with military adoption of Link 16 equipment, training simulators are being fitted with simulated tactical data links. The extensions made to Wireshark provide simulation engineers with a tool to troubleshoot Link 16 simulations.

Page classification:  UNCLASSIFIED

Navigation: previous [Testing and conclusions](03-testing-and-conclusions-pages-025-029.md) | [coverage index](README.md) | next none
