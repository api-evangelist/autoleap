# AutoLeap (autoleap)

AutoLeap is cloud-based shop management software for independent auto repair shops, covering repair orders, digital vehicle inspections, scheduling, parts ordering, invoicing, and reporting. Standard subscription plans (Essentials, Pro, Elite) are software-only and expose no public API. A separate, gated AutoLeap Partner API exists at [developers.myautoleap.com](https://developers.myautoleap.com/) - documented, versioned (v2), token-authenticated REST covering repair orders, customers, vehicles, appointments, inventory, items, payments, purchase orders, suppliers, and partner/company settings - but credentials (Partner ID and Auth Key) are only issued to approved integration partners on request, not to individual shop subscribers.

**Access model, in short:** this is not an open or self-serve developer API. It is a real, comprehensively documented REST API - but you have to be accepted as an AutoLeap partner (e.g. a parts supplier, payment processor, or franchise software vendor) to get credentials.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/autoleap/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/autoleap/refs/heads/main/apis.yml)

## Tags

- Auto Repair
- Shop Management
- Automotive
- Partner API
- Vertical SaaS

## Timestamps

- **Created:** 2026-07-04
- **Modified:** 2026-07-04

## APIs

### AutoLeap Repair Orders API

List, create, update, and fetch-by-RO-number repair orders (the estimate/invoice unit of work in a shop). Supports bulk create/update with a partial-success model, date-range filters on invoice/finalize/updated dates, and embedded appointment data.

- **Human URL:** [https://developers.myautoleap.com/openapi/repair-orders](https://developers.myautoleap.com/openapi/repair-orders)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `GET /repairOrders` - paginated list with filters
- `GET /repairOrders/{roNumber}` - single repair order
- `POST /repairOrders` - bulk create
- `PUT /repairOrders` - bulk update

### AutoLeap Customers API

Create, list, get, update, and archive shop customer records in bulk. Create and update operations are documented as beta and may still change shape.

- **Human URL:** [https://developers.myautoleap.com/openapi/customers](https://developers.myautoleap.com/openapi/customers)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `POST /customers` - bulk create (beta)
- `GET /customers` - paginated list
- `GET /customers/{customerId}` - single customer
- `PUT /customers` - bulk update (beta)
- `PATCH /customers` - bulk archive

### AutoLeap Vehicles API

Create, list, get, update, and archive customer vehicle records in bulk, including filtering, searching, and sorting on the list endpoint.

- **Human URL:** [https://developers.myautoleap.com/openapi/vehicles](https://developers.myautoleap.com/openapi/vehicles)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `POST /vehicles` - bulk create
- `GET /vehicles` - paginated list with filtering/searching/sorting
- `GET /vehicles/{vehicleId}` - single vehicle
- `PUT /vehicles` - bulk update
- `PATCH /vehicles` - bulk archive (sets vehicleStatus to Inactive)

### AutoLeap Appointments API

Create and bulk-update scheduled appointments, plus a separate appointment-requests flow (create requests, list requests, and check available booking slots) used for customer-facing scheduling integrations.

- **Human URL:** [https://developers.myautoleap.com/openapi/appointments](https://developers.myautoleap.com/openapi/appointments)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `GET /appointments` - list
- `POST /appointments` - bulk create
- `PUT /appointments` - bulk update
- `POST /appointmentRequests/create` - create a request
- `GET /appointmentRequests` - list requests
- `GET /appointmentRequests/availableSlots` - available booking slots

### AutoLeap Inventory & Items API

Create, list, get, update, and archive items (parts, tires, labor), plus read-only inventory-level and item-pricing lookups for parts and inventory system integrations.

- **Human URL:** [https://developers.myautoleap.com/openapi/items](https://developers.myautoleap.com/openapi/items)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `POST /items` - bulk create
- `GET /items` - list
- `GET /items/{itemId}` - single item
- `PUT /items` - bulk update
- `PATCH /items` - bulk archive
- `GET /inventoryLevels`, `GET /inventoryLevels/{itemId}`, `PUT /inventoryLevels/update`
- `GET /itemPricing`, `GET /itemPricing/{itemId}`

### AutoLeap Payments & Purchasing API

Read payments taken against repair orders for reconciliation and financial reporting, plus read purchase orders, supplier accounts-payable terms, and the supplier directory used to resolve supplier IDs.

- **Human URL:** [https://developers.myautoleap.com/openapi/payments](https://developers.myautoleap.com/openapi/payments)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `GET /payments` - paginated list
- `GET /purchaseOrders`, `GET /purchaseOrders/{id}`
- `GET /paymentTerms`
- `GET /suppliers`

### AutoLeap Shop Operations API

Supporting read endpoints for an integration's own account and a shop's operational reference data - partner profile (companies/locations the partner can access), staff/user roster, technician timesheet logs, canned service packages, tire storage records, and tax settings.

- **Human URL:** [https://developers.myautoleap.com/openapi/profile](https://developers.myautoleap.com/openapi/profile)
- **Base URL:** `https://partnerapi.myautoleap.com/v2`

#### Endpoints

- `GET /partners/profile`
- `GET /settings/users`
- `GET /technicians/timesheetLogs`
- `GET /cannedservices`, `POST /cannedservices`
- `GET /tireStorage`, `GET /tireStorage/{id}`
- `GET /taxes`

## Authentication

Token-based. Exchange a Partner ID and Auth Key at `POST /partners/login` for an `accessToken` (1 hour) and `refreshToken` (3 hours); refresh via `POST /partners/generateNewAccessToken` (recommended every ~55 minutes) rather than re-authenticating; `POST /partners/logout` invalidates the refresh token. All requests carry `Authorization: Bearer <accessToken>`.

Per the docs: *"This information is for AutoLeap Partners and is currently not available for Essentials, Pro, and Elite plans."* Credentials are requested from an AutoLeap contact, not self-served.

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/autoleap)
- [Website](https://autoleap.com/)
- [Documentation](https://developers.myautoleap.com/)
- [Plans](plans/autoleap-plans-pricing.yml)
- [Rate Limits](rate-limits/autoleap-rate-limits.yml)
- [Fin Ops](finops/autoleap-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
