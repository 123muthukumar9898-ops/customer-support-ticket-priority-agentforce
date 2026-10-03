# Test Cases

| Test | Input | Expected | Actual / evidence | Status |
|---|---|---|---|---|
| TC-1 | TKT-0003; subject `payment failed refund`; category Refund; Paid | Critical, 90, Billing Support | Critical, 90, Billing Support | Pass |
| TC-2 | TKT-0007; subject `app crash on checkout`; category Technical Issue; Paid | Critical, 90, Technical Support | Critical, 90, Technical Support | Pass |
| TC-3 | TKT-0004; subject `how to change profile`; category Other; Free | Low, 20, Technical Support | Low, 20, Technical Support | Pass |
| TC-4 | Existing test Account whose ticket description contains `urgent` | GetAccount/GetTicket succeed; High Priority path | Debug log retrieved records and ran High Priority | Pass |
| TC-5 | Non-existent/wrongly spelled Account Name | No account; default Low | Debug log showed no GetAccount record and Low path | Pass |
| TC-6 | Agent user asks for support ticket data | Agent asks for Account Name | Agent asks for Account Name | Pass (first step) |
| TC-7 | Ask how an urgent server-down ticket is prioritized/assigned | Agent runs priority Flow action | Earlier test showed clarifying question before the action was added | Partial in the report |

## Performance recorded in the report

- Autolaunched Flow: 1.25 seconds in Flow Debug.
- No-account run: 1.87 seconds.
- Record-triggered Flow writes the result when a new ticket is saved.
