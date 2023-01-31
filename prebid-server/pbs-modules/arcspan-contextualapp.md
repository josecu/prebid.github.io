---
layout: page_v2
page_type: pbs-module
title: Prebid Server ArcSpan Module
display_name : ArcSpan Contextual APP Module
sidebarType : 5
---

# ArcSpan Contextual APP Module
{:.no_toc}

* TOC
{:toc }

## Overview

This module attaches contextual classification signals to the site object in the bid request, with the goal of enhancing the addressability of ad impressions and increasing buyer demand.

## Configuration

### Execution Plan

### Global Config

The module needs to be enabled in the global config in order for it to be called.

{: .alert.alert-danger :}
The execution plan should be defined at the account level.

#### PBS.Go

Enable the module in `pbs.yaml`.

```
hooks:
  enabled: true
  modules:
    arcspan:
      contextualapp:
        enabled: true
```

#### PBS.Java

Coming soon

### Account-Level Config

This module runs at the processed auction request stage. It should be enabled for each of the following endpoints for maximum coverage:

- /openrtb2/auction
- /openrtb2/amp
- /openrtb2/video

This module should only be configured for accounts with an ArcSpan account. A silo parameter needs to be populated for the account with a value provided by an ArcSpan representative. This will ensure that ArcSpan can load the correct contextual signals for the account.

{: .alert.alert-warning :}
Please replace `YOUR_SILO_ID_HERE` with the account's ArcSpan silo ID.

#### PBS.Go

```
{
   "id":"1001",
   "disabled":false,
   "hooks":{
      "modules":{
         "arcspan":{
            "contextualapp":{
               "silo":"YOUR_SILO_ID_HERE"
            }
         }
      },
      "execution_plan":{
         "endpoints":{
            "/openrtb2/auction":{
               "stages":{
                  "processed_auction_request":{
                     "groups":[
                        {
                           "timeout":5000,
                           "hook_sequence":[
                              {
                                 "module_code":"arcspan.contextualapp",
                                 "hook_impl_code":"arcspan_processed_auction_request_hook"
                              }
                           ]
                        }
                     ]
                  }
               }
            },
            "/openrtb2/amp":{
               "stages":{
                  "processed_auction_request":{
                     "groups":[
                        {
                           "timeout":5000,
                           "hook_sequence":[
                              {
                                 "module_code":"arcspan.contextualapp",
                                 "hook_impl_code":"arcspan_processed_auction_request_hook"
                              }
                           ]
                        }
                     ]
                  }
               }
            },
            "/openrtb2/video":{
               "stages":{
                  "processed_auction_request":{
                     "groups":[
                        {
                           "timeout":5000,
                           "hook_sequence":[
                              {
                                 "module_code":"arcspan.contextualapp",
                                 "hook_impl_code":"arcspan_processed_auction_request_hook"
                              }
                           ]
                        }
                     ]
                  }
               }
            }
         }
      }
   }
}
```

#### PBS.Java

Coming soon