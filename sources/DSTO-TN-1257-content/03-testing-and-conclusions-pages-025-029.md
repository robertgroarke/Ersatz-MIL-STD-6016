# Testing and conclusions

Source: `DSTO-TN-1257.pdf`, PDF pages 25-29.

Navigation: previous [Wireshark dissector design and implementation](02-wireshark-dissector-design-and-implementation-pages-016-024.md) | [coverage index](README.md) | next [Appendices and sample capture](04-appendices-and-sample-capture-pages-030-041.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-25"></a>

## Source PDF page 25

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

17 2013. */ +const value_string Link16_NPG_Strings[] = { +    { 1, "Initial Entry" },

### +    { 2, "RTT-A" },

### +    { 3, "RTT-B" },

+    { 4, "Network Management" }, +    { 5, "PPLI and Status" }, +    { 6, "PPLI and Status" }, +    { 7, "Surveillance" }, +    { 8, "Mission Management/Weapons Coordination" }, +    { 9, "Control" }, +    { 11, "Image Transfer" }, +    { 12, "Voice A" }, +    { 13, "Voice B" }, +    { 18, "Network Enabled Weapons" }, +    { 19, "Figher-to-Fighter A" }, +    { 20, "Figher-to-Fighter B" }, +    { 21, "Engagement Coordination" }, +    { 27, "Joint Net PPLI" }, +    { 28, "Distributed Network Management" },

### +    { 0, NULL },

+}; + +static int proto_link16 = -1; + +static dissector_handle_t link16_handle; + +static gint hf_link16_wordformat = -1; +static gint hf_link16_label = -1; +static gint hf_link16_sublabel = -1; +static gint hf_link16_mli = -1; +static gint hf_link16_contlabel = -1; + +static gint ett_link16 = -1; + +static void dissect_link16(tvbuff_t *tvb, packet_info *pinfo, proto_tree *tree) +{ +    proto_item *link16_item = NULL; +    proto_tree *link16_tree = NULL; +    guint32 cache; +    guint8 wordformat, contlabel, mli; + +    Link16State *state = (Link16State*)pinfo->private_data; +    if (!state) { +        REPORT_DISSECTOR_BUG("Link 16 dissector state missing"); +    } + +    cache = tvb_get_letohl(tvb, 0); +    wordformat = cache & 0x3; + +    col_set_str(pinfo->cinfo, COL_PROTOCOL, "Link 16"); + +    if (tree) { +        link16_item = proto_tree_add_item(tree, proto_link16, tvb, 0, -1, TRUE); +        link16_tree = proto_item_add_subtree(link16_item, ett_link16); +        proto_tree_add_uint(link16_tree, hf_link16_wordformat, tvb, 0, 0, wordformat); +    } + +    /* Elmasry, G., (2012), Tactical Wireless Communications and Networks: Design Concepts and Challenges, Wiley, ISBN 9781119951766. */ +    if (wordformat == WORDFORMAT_INITIAL) { +        state->label     = (cache >> 2) & 0x1F; +        state->sublabel  = (cache >> 7) & 0x7; +        state->extension = 0; +        mli = (cache >> 10) & 0x7; +        col_append_fstr(pinfo->cinfo, COL_INFO, " J%d.%dI", state->label, state->sublabel);

+        if (tree) { +            proto_item_append_text(link16_item, " J%d.%dI", state->label, state->sublabel); +            proto_tree_add_uint(link16_tree, hf_link16_label, tvb, 0, 0, state->label); +            proto_tree_add_uint(link16_tree, hf_link16_sublabel, tvb, 0, 0, state- >sublabel);

<a id="source-pdf-page-26"></a>

## Source PDF page 26

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

18 +            proto_tree_add_uint(link16_tree, hf_link16_mli, tvb, 0, 0, mli); +        } +    } else if (wordformat == WORDFORMAT_EXTENSION) { +        col_append_fstr(pinfo->cinfo, COL_INFO, " J%d.%dE%d", state->label, state- >sublabel, state->extension); +        if (tree) +           proto_item_append_text(link16_item, " J%d.%dE%d", state->label, state->sublabel, state->extension); +        state->extension++; +    } else if (wordformat == WORDFORMAT_CONTINUATION) { +        contlabel = (cache >> 2) & 0x1F; +        proto_tree_add_uint(link16_tree, hf_link16_contlabel, tvb, 0, 0, contlabel); +        col_append_fstr(pinfo->cinfo, COL_INFO, " J%d.%dC%d", state->label, state- >sublabel, contlabel); +        if (tree) +            proto_item_append_text(link16_item, " J%d.%dC%d", state->label, state- >sublabel, contlabel); +    } else { +        return; +    } + +    proto_item_append_text(link16_item, " %s", val_to_str_const(MKPAIR(state->label, state- >sublabel), Link16_Message_Strings, "Unknown")); +} + +void proto_register_link16(void) +{ +    static hf_register_info hf[] = { +        { &hf_link16_wordformat, +          { "Word Format", "link16.wordformat", FT_UINT8, BASE_DEC, VALS(WordFormat_Strings), 0x0,

### +            NULL, HFILL }},

+        { &hf_link16_label, +          { "Label", "link16.label", FT_UINT8, BASE_DEC, VALS(Link16_Label_Strings), 0x0,

### +            NULL, HFILL }},

+        { &hf_link16_sublabel, +          { "Sublabel", "link16.sublabel", FT_UINT8, BASE_DEC, NULL, 0x0,

### +            NULL, HFILL }},

+        { &hf_link16_mli, +          { "Message Length Indicator", "link16.mli", FT_UINT8, BASE_DEC, NULL, 0x0,

### +            NULL, HFILL }},

+        { &hf_link16_contlabel, +          { "Continuation Word Label", "link16.contlabel", FT_UINT8, BASE_DEC, NULL, 0x0,

### +            NULL, HFILL }}

+    }; +    static gint *ett[] = { +        &ett_link16, +    }; + +    proto_link16 = proto_register_protocol("Link 16", "LINK16", "link16"); +    proto_register_field_array(proto_link16, hf, array_length (hf)); +    proto_register_subtree_array(ett, array_length(ett)); +    register_dissector("link16", dissect_link16, proto_link16); +} + +void proto_reg_handoff_link16(void) +{ +    link16_handle = create_dissector_handle(dissect_link16, proto_link16); +} diff --git a/epan/dissectors/packet-link16.h b/epan/dissectors/packet-link16.h new file mode 100644 index 0000000..9df0d4f --- /dev/null +++ b/epan/dissectors/packet-link16.h @@ -0,0 +1,34 @@ +/* packet-link16.h + * Routines for Link 16 message dissection (MIL-STD-6016) + * William Robertson <aliask@gmail.com> + * Peter Ross <peter.ross@dsto.defence.gov.au> + * + * $Id$

<a id="source-pdf-page-27"></a>

## Source PDF page 27

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

19 + * + * This program is free software; you can redistribute it and/or + * modify it under the terms of the GNU General Public License + * as published by the Free Software Foundation; either version 2 + * of the License, or (at your option) any later version. + * + * This program is distributed in the hope that it will be useful, + * but WITHOUT ANY WARRANTY; without even the implied warranty of + * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the + * GNU General Public License for more details. + * + * You should have received a copy of the GNU General Public License + * along with this program; if not, write to the Free Software + * Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA + */ + +#ifndef __PACKET_LINK16_H__ +#define __PACKET_LINK16_H__ + +#include <epan/value_string.h> + +extern const value_string Link16_NPG_Strings[]; + +typedef struct { +    gint label, sublabel, extension; +} Link16State; + +#endif /* __PACKET_LINK16_H__ */ -- 1.8.1.2

### Figure A1: Software patch (part 1 of 3)

From 93afe993b7f801c6a8b761c978bbdc26cf7bca06 Mon Sep 17 00:00:00 2001 From: Peter Ross <peter.ross@dsto.defence.gov.au> Date: Wed, 16 Oct 2013 10:00:02 +1100 Subject: [PATCH 2/3] packet-dis: SISO-J Link 16 PDU dissector (SISO-STD-002)

--epan/dissectors/packet-dis-enums.c  |  20 +++++ epan/dissectors/packet-dis-enums.h  |  16 ++++ epan/dissectors/packet-dis-fields.c |  33 +++++-epan/dissectors/packet-dis-fields.h |  24 ++++epan/dissectors/packet-dis-pdus.c   | 170 ++++++++++++++++++++++++++++++-----epan/dissectors/packet-dis-pdus.h   |   2 +epan/dissectors/packet-dis.c        |  74 +++++++++++++---

### 7 files changed, 293 insertions(+), 46 deletions(-)

diff --git a/epan/dissectors/packet-dis-enums.c b/epan/dissectors/packet-dis-enums.c index 73d8264..d53b3a7 100644 --- a/epan/dissectors/packet-dis-enums.c +++ b/epan/dissectors/packet-dis-enums.c @@ -453,6 +453,25 @@ const value_string DIS_PDU_MajorModulation_Strings[] =

### {0,                                      NULL }

};

+const range_string DIS_PDU_Link16_CVLL_Strings[] = { +    { 0,   127, "Crypto Variable" },

### +    { 255, 255, "NO STATEMENT" },

### +    { 0,   0,   NULL }

+}; + +const value_string DIS_PDU_Link16_MessageType_Strings[] = +{ +    { DIS_MESSAGE_TYPE_JTIDS_HEADER_MESSAGES, "JTIDS Header/Messages" },

### +    { DIS_MESSAGE_TYPE_RTT_A_B,               "RTT A/B" },

+    { DIS_MESSAGE_TYPE_RTT_REPLY,             "RTT Reply" }, +    { DIS_MESSAGE_TYPE_JTIDS_VOICE_CVSD,      "JTIDS Voice CVSD" }, +    { DIS_MESSAGE_TYPE_JTIDS_VOICE_LPC10,     "JTIDS Voice LPC10" },

<a id="source-pdf-page-28"></a>

## Source PDF page 28

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

20 +    { DIS_MESSAGE_TYPE_JTIDS_VOICE_LPC12,     "JTIDS Voice LPC12" },

### +    { DIS_MESSAGE_TYPE_JTIDS_LET,             "JTIDS LET" },

### +    { DIS_MESSAGE_TYPE_VMF,                   "VMF" },

### +    { 0,                                      NULL }

+}; + const value_string DIS_PDU_EmissionFunction_Strings[] = { {DIS_EMISSION_FUNCTION_OTHER,                    "Other" }, @@ -663,6 +682,7 @@ const value_string DIS_PDU_TerminalSecondaryMode_Strings[] =

### {0,    NULL }

};

+/* http://discussions.sisostds.org/threadview.aspx?fid=18&threadid=53172 */ const value_string DIS_PDU_ModParamSyncState_Strings[] = { {0,    "Undefined" }, diff --git a/epan/dissectors/packet-dis-enums.h b/epan/dissectors/packet-dis-enums.h index 913eb1f..0ab3b96 100644 --- a/epan/dissectors/packet-dis-enums.h +++ b/epan/dissectors/packet-dis-enums.h @@ -48,6 +48,8 @@ extern const value_string DIS_PDU_TSAllocationFidelity_Strings[]; extern const value_string DIS_PDU_TerminalPrimaryMode_Strings[]; extern const value_string DIS_PDU_TerminalSecondaryMode_Strings[]; extern const value_string DIS_PDU_ModParamSyncState_Strings[]; +extern const range_string DIS_PDU_Link16_CVLL_Strings[]; +extern const value_string DIS_PDU_Link16_MessageType_Strings[];

typedef enum @@ -438,6 +440,20 @@ extern const value_string DIS_PDU_MajorModulation_Strings[];

typedef enum {

### +    DIS_MESSAGE_TYPE_JTIDS_HEADER_MESSAGES = 0,

### +    DIS_MESSAGE_TYPE_RTT_A_B,

### +    DIS_MESSAGE_TYPE_RTT_REPLY,

### +    DIS_MESSAGE_TYPE_JTIDS_VOICE_CVSD,

### +    DIS_MESSAGE_TYPE_JTIDS_VOICE_LPC10,

### +    DIS_MESSAGE_TYPE_JTIDS_VOICE_LPC12,

### +    DIS_MESSAGE_TYPE_JTIDS_LET,

### +    DIS_MESSAGE_TYPE_VMF

+} DIS_PDU_MessageType; + +extern const value_string DIS_PDU_JTIDS_MessageType_Strings[]; + +typedef enum +{

### DIS_EMISSION_FUNCTION_OTHER                         = 0,

### DIS_EMISSION_FUNCTION_MULTI_FUNCTION                = 1,

### DIS_EMISSION_FUNCTION_EARLY_WARNING_SURVEILLANCE    = 2,

diff --git a/epan/dissectors/packet-dis-fields.c b/epan/dissectors/packet-dis-fields.c index 2b2007f..c6d7440c 100644 --- a/epan/dissectors/packet-dis-fields.c +++ b/epan/dissectors/packet-dis-fields.c @@ -43,7 +43,9 @@ guint32 category; guint32 radioID; guint32 disRadioTransmitState; guint32 encodingScheme; +guint32 tdlType; guint32 numSamples; +guint32 messageType; guint32 numFixed; guint32 numVariable; guint32 numBeams; @@ -209,6 +211,20 @@ DIS_ParserNode DIS_FIELDS_MOD_PARAMS_JTIDS_MIDS[] =

### { DIS_FIELDTYPE_END,                          NULL,0,0,0,0 }

};

+DIS_ParserNode DIS_FIELDS_SIGNAL_LINK16_NETWORK_HEADER[] = +{

<a id="source-pdf-page-29"></a>

## Source PDF page 29

### UNCLASSIFIED

### DSTO-TN-1257

### UNCLASSIFIED

21 +    { DIS_FIELDTYPE_LINK16_NPG,          "Network Participant Group",0,0,0,0 }, +    { DIS_FIELDTYPE_UINT8,               "Network Number",0,0,0,0 },

### +    { DIS_FIELDTYPE_LINK16_TSEC_CVLL,    "TSEC CVLL",0,0,0,0 },

### +    { DIS_FIELDTYPE_LINK16_MSEC_CVLL,    "MSEC CVLL",0,0,0,0 },

+    { DIS_FIELDTYPE_LINK16_MESSAGE_TYPE, "Message Type",0,0,0,&messageType }, +    { DIS_FIELDTYPE_UINT16,              "Padding",0,0,0,0 }, +    { DIS_FIELDTYPE_UINT32,              "Time Slot ID",0,0,0,0 }, +    { DIS_FIELDTYPE_LINK16_PTT,          "Perceived Transmit Time",0,0,0,0 }, +    { DIS_FIELDTYPE_LINK16_MESSAGE_DATA, "Message Data",0,0,0,0 },

### +    { DIS_FIELDTYPE_END,                 NULL,0,0,0,0 }

+}; + /* Array records */ DIS_ParserNode DIS_FIELDS_FIXED_DATUM[] = @@ -513,6 +529,7 @@ void initializeFieldParsers(void) initializeParser(DIS_FIELDS_VR_UA_BEAM); initializeParser(DIS_FIELDS_MOD_PARAMS_CCTT_SINCGARS); initializeParser(DIS_FIELDS_MOD_PARAMS_JTIDS_MIDS); +    initializeParser(DIS_FIELDS_SIGNAL_LINK16_NETWORK_HEADER);

}

@@ -868,6 +885,10 @@ gint parseField_Enum(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_ParserNod break; } break; +    case DIS_FIELDTYPE_LINK16_MESSAGE_TYPE: +        enumStrings = DIS_PDU_Link16_MessageType_Strings; +        dis_hf_id = hf_dis_signal_link16_message_type; +        break; default: enumStrings = 0; break; @@ -1019,7 +1040,7 @@ gint parseField_Timestamp(tvbuff_t *tvb, proto_tree *tree, gint offset, DIS_Pars

/* Parse a variable parameter field. */ -gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree, gint offset) +gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree , gint offset, packet_info *pinfo) { DIS_ParserNode *paramParser = 0;

@@ -1045,7 +1066,7 @@ gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree, gint offset) /* Parse the variable parameter fields */ if (paramParser) { -        offset = parseFields(tvb, tree, offset, paramParser); +        offset = parseFields(tvb, tree, offset, paramParser, pinfo); }

return offset; @@ -1053,7 +1074,7 @@ gint parseField_VariableParameter(tvbuff_t *tvb, proto_tree *tree, gint offset)

/* Parse a variable record field. */ -gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset) +gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset, packet_info *pinfo) { DIS_ParserNode *paramParser = 0;

@@ -1086,7 +1107,7 @@ gint parseField_VariableRecord(tvbuff_t *tvb, proto_tree *tree, gint offset) /* Parse the variable record fields */ if (paramParser)

Navigation: previous [Wireshark dissector design and implementation](02-wireshark-dissector-design-and-implementation-pages-016-024.md) | [coverage index](README.md) | next [Appendices and sample capture](04-appendices-and-sample-capture-pages-030-041.md)
