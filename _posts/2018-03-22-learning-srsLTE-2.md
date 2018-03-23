---
layout: post
title: Learning srsLTE - 2
description: srsLTE data structure overview and references.
permalink: /learning-srslte-2/
categories: [blog]
tags: [srslte, software radio, software, library]
date: 2018-03-22 17:34:56
---

# Introduction

There are so many API provided by srsLTE library. One can find an API document of srsLTE provided by the well-known [ShareTechNote](http://www.sharetechnote.com/) website, including

-   [API description](http://www.sharetechnote.com/html/SDR_srsLTE_Api.html)
-   [Data structure description](http://www.sharetechnote.com/html/SDR_srsLTE_Api_TypeDef.html)

Though the website is comprehensive and detailed, I think the web page was not well-rendered, especially the code. Using sans-serif non-monospaced fonts for the code is not a good practice, isn't it? By the way, the data structure page does not have anchor links to navigate.

In this document, I will give a reference to the structure type definition. I'll leave the API functions to the following posts.

**Physical layer data structure will be in another post!**

# Shortcuts

## ASN.1

## Common

## Interfaces

## Radio

## Upper

# Data Structures

## ASN.1

ASN.1 means "Abstract Syntax Notation One". See more at [Wikipedia](https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One).

---

### gtpc\_header

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef struct gtpc_header
{
  uint8_t version;
  bool piggyback;
  bool teid_present;
  uint8_t type;
  uint64_t teid;
  uint64_t sequence;
} gtpc_header_t;
```

Read more: [GPRS Tunnelling Protocol - Wikipedia](https://en.wikipedia.org/wiki/GPRS_Tunnelling_Protocol).

### gtpc\_msg\_choice

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef union gtpc_msg_choice
{
  struct gtpc_create_session_request create_session_request;
  struct gtpc_create_session_response create_session_response;
  struct gtpc_modify_bearer_request modify_bearer_request;
  struct gtpc_modify_bearer_response modify_bearer_response;
  struct gtpc_delete_session_request delete_session_request;
  struct gtpc_delete_session_response delete_session_response;
} gtpc_msg_choice_t; 
```

### gtpc\_pdu

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef struct gtpc_pdu
{
  struct gtpc_header header;
  union gtpc_msg_choice choice;
} gtpc_pdu_t;
```

### gtpc\_cause\_ie

Location: `./lib/include/srslte/asn1/gtpc_ies.h`

```c++
struct gtpc_cause_ie
{
  enum gtpc_cause_value cause_value;
  bool pce;
  bool bce;
  bool cs;
  enum gtpc_ie_type offending_ie_type;
  uint16_t length_of_offending_ie;
  uint8_t offending_ie_instance;
};
```

Other data structure defined in this file: `enum gtpc_ie_type`, `enum gtpc_cause_value`, `struct gtpc_ambr_ie`, `enum gtpc_pdn_type`, `struct gtpc_pdn_address_allocation_ie`, `enum gtpc_rat_type`, `enum gtpc_interface_type`, `struct gtpc_f_teid_ie`.

### gtpc\_create\_session\_request

Location: `./lib/include/srslte/asn1/gtpc_msg.h`

```c++
struct gtpc_create_session_request
{
  bool imsi_present;
  uint64_t imsi;   						// C

  enum gtpc_rat_type rat_type;					// M

  struct gtpc_f_teid_ie sender_f_teid;					// M
  bool pgw_addr_present;
  struct gtpc_f_teid_ie pgw_addr;					// C

  char apn[MAX_APN_LENGTH];							// M

  struct gtpc_bearer_context_created_ie //see  TS 29.274 v10.14.0 Table 7.2.1-2
  {
    uint8_t ebi;
    bool tft_present;
    bool s1_u_enodeb_f_teid_present;
    struct gtpc_f_teid_ie s1_u_enodeb_f_teid;
    bool s4_u_sgsn_f_teid_present;
    struct gtpc_f_teid_ie s4_u_sgsn_f_teid;
    bool s5_s8_u_sgw_f_teid_present;
    struct gtpc_f_teid_ie s5_s8_u_sgw_f_teid;
    bool s5_s8_u_pgw_f_teid_present;
    struct gtpc_f_teid_ie s5_s8_u_pgw_f_teid;
    bool s12_rnc_f_teid_present;
    struct gtpc_f_teid_ie s12_rnc_f_teid;
    bool s2b_u_epdg_f_teid_present;
    struct gtpc_f_teid_ie s2b_u_epdg_f_teid;
  } eps_bearer_context_created;		// M
};
```

Other data structure defined in this file: `struct gtpc_create_session_response`, `struct gtpc_modify_bearer_request`, `struct gtpc_modify_bearer_response`, `struct gtpc_delete_session_request`, `struct gtpc_delete_session_response`.

### 

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++

```

### 

Location: `./lib/include/srslte/asn1/liblte_mme.h`

```c++

```

### 

Location: `./lib/include/srslte/asn1/liblte_rrc.h`

```c++

```

### 

Location: `./lib/include/srslte/asn1/liblte_s1ap.h`

```c++

```

### 

Location: `./lib/include/srslte/common/bcd_helpers.h`

```c++

```

### 

Location: `./lib/include/srslte/common/block_queue.h`

```c++

```

### 

Location: `./lib/include/srslte/common/buffer_pool.h`

```c++

```

### 

Location: `./lib/include/srslte/common/common.h`

```c++

```

### 

Location: `./lib/include/srslte/common/config.h`

```c++

```

### 

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++

```

### 

Location: `./lib/include/srslte/common/liblte_security.h`

```c++

```

### 

Location: `./lib/include/srslte/common/liblte_ssl.h`

```c++

```

### 

Location: `./lib/include/srslte/common/log.h`

```c++

```

### 

Location: `./lib/include/srslte/common/logger.h`

```c++

```

### 

Location: `./lib/include/srslte/common/logger_file.h`

```c++

```

### 

Location: `./lib/include/srslte/common/logger_stdout.h`

```c++

```

### 

Location: `./lib/include/srslte/common/log_filter.h`

```c++

```

### 

Location: `./lib/include/srslte/common/mac_pcap.h`

```c++

```

### 

Location: `./lib/include/srslte/common/metrics_hub.h`

```c++

```

### 

Location: `./lib/include/srslte/common/msg_queue.h`

```c++

```

### 

Location: `./lib/include/srslte/common/nas_pcap.h`

```c++

```

### 

Location: `./lib/include/srslte/common/pcap.h`

```c++

```

### 

Location: `./lib/include/srslte/common/pdu.h`

```c++

```

### 

Location: `./lib/include/srslte/common/pdu_queue.h`

```c++

```

### 

Location: `./lib/include/srslte/common/security.h`

```c++

```

### 

Location: `./lib/include/srslte/common/snow_3g.h`

```c++

```

### 

Location: `./lib/include/srslte/common/task_dispatcher.h`

```c++

```

### 

Location: `./lib/include/srslte/common/threads.h`

```c++

```

### 

Location: `./lib/include/srslte/common/thread_pool.h`

```c++

```

### 

Location: `./lib/include/srslte/common/timeout.h`

```c++

```

### 

Location: `./lib/include/srslte/common/timers.h`

```c++

```

### 

Location: `./lib/include/srslte/common/trace.h`

```c++

```

### 

Location: `./lib/include/srslte/common/tti_sync.h`

```c++

```

### 

Location: `./lib/include/srslte/common/tti_sync_cv.h`

```c++

```

### 

Location: `./lib/include/srslte/interfaces/enb_interfaces.h`

```c++

```

### 

Location: `./lib/include/srslte/interfaces/enb_metrics_interface.h`

```c++

```

### 

Location: `./lib/include/srslte/interfaces/epc_interfaces.h`

```c++

```

### 

Location: `./lib/include/srslte/interfaces/sched_interface.h`

```c++

```

### 

Location: `./lib/include/srslte/interfaces/ue_interfaces.h`

```c++

```

### 

Location: `./lib/include/srslte/radio/radio.h`

```c++

```

### 

Location: `./lib/include/srslte/radio/radio_multi.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/gtpu.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/pdcp.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/pdcp_entity.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_am.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_entity.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_interface.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_metrics.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_tm.h`

```c++

```

### 

Location: `./lib/include/srslte/upper/rlc_um.h`

```c++

```
