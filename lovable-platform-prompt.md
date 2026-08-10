# Lovable build prompt — GEAI application

Build a production-quality authenticated web application for **GEAI — Green Energy Artificial Intelligence** and visually match the existing public site at https://innovation-guide-box.lovable.app/.

The existing public marketing website remains the landing page. This new application is the authenticated product console and should be deployable as `app.geai.ai` or linked from the existing `/sign-in` page.

## Design direction

Use the visual language of the public GEAI website: premium climate-tech / energy SaaS, dark forest green, warm off-white backgrounds, fresh green accents, precise typography, subtle borders, restrained shadows, dense but readable operational dashboards. Avoid generic neon AI aesthetics. The product should feel credible for utilities, IPPs, EPCs, O&M organizations, and asset managers.

## Authentication and roles

Use Lovable Cloud / Supabase Auth. Support email/password now, with schema ready for SSO and MFA.

Implement multi-tenant organization membership and RBAC with these roles:
- platform_admin
- org_admin
- asset_manager
- operator
- engineer
- technician
- viewer

A user can belong to one or more organizations. All tenant data must be protected with Row-Level Security.

## Application shell

Left sidebar, sticky top bar, organization switcher, notifications, profile menu, responsive mobile drawer.

Operator navigation:
1. Overview
2. Sites & Assets
3. Forecasting
4. Diagnostics
5. Maintenance
6. IoT Sensors
7. Virtual Energy Expert
8. Installation Advisor
9. Reports
10. Settings

Platform Admin navigation:
1. Admin Overview
2. Organizations
3. Users & Roles
4. Asset Registry
5. Data Integrations
6. AI Models
7. Sensor Fleet
8. Alert Policies
9. System Health
10. Plans & Billing
11. Audit Log
12. Platform Settings

## Operator Overview

Create a professional renewable-energy command center with:
- online capacity
- performance ratio
- availability
- recovered energy
- generation vs AI forecast chart
- AI-prioritized anomaly list
- fleet/site health
- open work orders
- weather-risk summary
- compact Virtual Energy Expert briefing

Use a realistic Uzbekistan demo portfolio with solar, wind, hybrid/storage, and commercial rooftop assets. Clearly label seeded data as demo data.

## Sites & Assets

Map + table + site detail views.

Each site detail should include:
- current output
- capacity
- availability
- performance ratio
- expected vs actual generation
- weather
- asset hierarchy
- inverter/turbine/battery status
- active anomalies
- maintenance history
- connected sensors
- financial loss/recovery estimates

Asset classes: solar plant, solar string, inverter, wind turbine, battery/BESS, smart meter, environmental sensor, gateway.

## Forecasting

Support portfolio and per-site forecasts for next 24h, 7d, 14d.

Show:
- P50 expected generation
- confidence interval
- weather inputs
- irradiance / wind-speed outlook
- forecast-vs-actual history
- MAE/MAPE
- expected revenue
- uncertainty alerts

Architecture should allow future Python AI models/API endpoints without embedding model logic in the browser.

## Diagnostics

AI anomaly center for:
- solar soiling
- shading
- degradation
- inverter faults
- string mismatch
- wind power-curve deviation
- yaw misalignment
- icing
- curtailment
- battery temperature / SOC issues
- sensor failure

Each finding requires:
- severity
- confidence score
- affected site/assets
- evidence
- estimated energy loss
- estimated revenue loss
- recommended action
- create-work-order action
- acknowledgement and status history

## Maintenance

Kanban/table views for work orders with priority, asset, assignee, deadline, status, AI-estimated recovery, notes, attachments, and before/after performance verification.

## IoT Sensors

Real-time-like sensor UI for GEAI-S1 devices with:
- ambient temperature
- panel surface temperature
- relative humidity
- illuminance/lux
- dust/PM
- wind speed/direction
- rainfall/snow
- battery
- signal quality
- sampling cadence
- gateway
- last-seen timestamp

Add device provisioning and connectivity status for MQTT, Modbus, OPC UA, and SCADA integrations.

## Virtual Energy Expert

Chat interface grounded in the organization’s operational data. Include sample prompts and citation/evidence cards. Responses must be able to reference sites, forecasts, anomalies, work orders, sensor data, and financial impact. Keep the backend abstracted behind an `/api/ai/chat` interface.

## Installation Advisor

Wizard for new solar/hybrid projects:
- location
- usable area
- orientation and tilt
- shading
- annual/interval consumption
- tariff
- panel/inverter assumptions
- optional battery

Results:
- recommended system size
- expected annual yield
- self-consumption
- battery sizing
- payback
- annual savings
- CO2 avoided
- assumptions and sensitivity

## Admin console

Platform-wide administration for all tenants. Include:
- organization creation and status
- subscription/plan
- per-tenant capacity/sites/users
- user invitations and role management
- asset registry
- integrations and connector health
- AI model registry with versions/stages/quality metrics
- IoT sensor/gateway fleet
- alert policies
- system health / API latency / ingestion / AI inference
- billing
- immutable audit log
- platform feature flags and defaults

## Database

Create Supabase tables and migrations for:
organizations, profiles, organization_members, sites, assets, telemetry_points, iot_devices, forecasts, anomalies, work_orders, weather_observations, reports, integrations, ai_models, alert_policies, audit_logs, subscriptions.

Include created_at/updated_at, UUID primary keys, tenant ownership, indexes, foreign keys, enum/status constraints where useful, and RLS policies.

Do not store high-frequency raw SCADA telemetry as a huge ordinary browser-facing table. Create abstractions/interfaces for time-series ingestion and a summarized telemetry table. The frontend should be ready to use TimescaleDB or an external time-series service later.

## Landing-page integration

Add a "Back to GEAI website" link in the login page and user menu. The existing public website's Sign In button should point to this application URL. Preserve `/product`, `/advisor`, `/pricing`, and public marketing content on the landing domain.

## Quality bar

- Fully responsive
- Accessible labels and keyboard states
- Real empty/loading/error states
- Skeleton loaders
- Toast notifications
- Search/filter/sort/pagination where appropriate
- Reusable components
- No duplicated page logic
- TypeScript
- Supabase typed client
- Environment variables for all API keys
- No secrets in frontend code
- Seed/demo dataset separated from production data
- No fake claims presented as actual customer performance

