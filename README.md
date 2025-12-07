# Invoice Processing Agent

  AI-powered invoice processing workflow built with n8n and Claude Sonnet 4.5.

  ## What It Does

  Automatically processes vendor invoices received via email, chat, or webhook:

  1. **Extracts** invoice data from PDFs using AI
  2. **Validates** PO numbers against a MySQL database
  3. **Determines** status: approved, missing PO, invalid PO, or insufficient balance
  4. **Generates** appropriate vendor response emails
  5. **Creates** NetSuite Vendor Bill (mock API) for approved invoices
  6. **Notifies** finance team via Slack with rich formatting

  ## Workflows

  | File | Description |
  |------|-------------|
  | `workflows/1-invoice-agent-no-hitl.json` | Fully automated flow |
  | `workflows/2-invoice-agent-with-hitl.json` | Includes Slack approval step |
  | `workflows/3-error-handler.json` | Error notifications to Slack |

  ## Flowcharts

  - [Without Human-in-the-Loop](https://miro.com/app/board/uXjVGeiyxqU=/?share_link_id=747582566205)
  - [With Human-in-the-Loop](https://miro.com/app/board/uXjVGfOvFU8=/?share_link_id=393319100919)

  ## Tech Stack

  - **Orchestration:** n8n
  - **AI Model:** Claude Sonnet 4.5 (Anthropic)
  - **Database:** [MySQL on Railway](https://railway.app)
  - **Notifications:** Slack Block Kit
  - **Email:** Gmail API

  ## Validation Scenarios

  | Scenario | Action |
  |----------|--------|
  | Missing PO | Request PO from vendor |
  | Invalid PO | Notify vendor, request correction |
  | Insufficient Balance | Notify vendor of shortfall, offer options |
  | Approved | Create Vendor Bill, send confirmation |

  ## Setup

  1. Import workflow JSONs into n8n
  2. Configure credentials:
     - Gmail OAuth
     - Slack OAuth
     - [MySQL on Railway](https://railway.app)
     - Anthropic API
  3. Create `po_data` table using [`database/schema.sql`](database/schema.sql)
  4. Test with sample invoice PDFs
