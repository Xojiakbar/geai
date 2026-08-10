# GEAI Platform MVP

A polished, responsive frontend MVP for the GEAI renewable-energy intelligence platform, designed to connect to the existing landing site:

https://geai.lovable.app/

## Included

### User / Operator workspace
- Overview dashboard
- Sites & asset registry
- AI generation forecasting
- AI diagnostics / anomaly detection
- Maintenance intelligence / work orders
- GEAI IoT sensor monitoring
- Virtual Energy Expert
- Installation Advisor
- Reports
- Workspace settings

### Admin workspace
- Admin overview / control plane
- Organizations / tenants
- Users & RBAC
- Global asset registry
- Data integrations
- AI model registry
- Sensor fleet administration
- Alert policies
- System health / observability
- Plans & billing
- Audit log
- Platform settings

## Demo

Open `index.html` in a browser, or serve this folder with any static server.

Example:

```bash
python3 -m http.server 8080
```

Then open http://localhost:8080

Demo buttons on the login page switch between:
- Operator workspace
- Admin workspace

This is a frontend prototype. The current login is intentionally demo-only and must be replaced by real authentication before production deployment.

## Connect it to the existing Lovable landing page

Recommended production setup:

- Marketing: `https://geai.ai` (or the existing Lovable domain)
- Application: `https://app.geai.ai`
- API: `https://api.geai.ai`

Change the existing landing-page **Sign in** button to:

```text
https://app.geai.ai
```

Change **Explore the platform** to either the application URL or keep `/product` as the public product page and add a secondary **Open platform** CTA.

## Recommended backend for production

For the fastest Lovable-native implementation, use Supabase/Lovable Cloud for:

- Auth + MFA
- PostgreSQL database
- Row-Level Security
- Organization / user roles
- Storage for reports and asset files
- Edge Functions for API orchestration

Recommended main tables:

- `organizations`
- `profiles`
- `organization_members`
- `sites`
- `assets`
- `telemetry_points`
- `iot_devices`
- `forecasts`
- `anomalies`
- `work_orders`
- `weather_observations`
- `reports`
- `integrations`
- `ai_models`
- `alert_policies`
- `audit_logs`
- `subscriptions`

### Suggested roles
- `platform_admin`
- `org_admin`
- `asset_manager`
- `operator`
- `engineer`
- `technician`
- `viewer`

## Production architecture

```text
GEAI Landing Page
      |
      +---- app.geai.ai
               |
          Auth / RBAC
               |
         GEAI Web App
               |
        API / Edge Layer
          /    |     \
     DB     AI API   Data Ingestion
              |       /   |   \
          Forecast  MQTT OPC-UA SCADA
          Anomaly
          Copilot
```

For utility-scale deployments, telemetry should not be written directly from SCADA devices to the browser or Supabase. Use an ingestion/API service or secure edge gateway, with time-series storage (for example TimescaleDB) and asynchronous AI jobs.

## Next integration steps

1. Deploy this app to a frontend host or Lovable project.
2. Connect Supabase/Lovable Cloud authentication.
3. Add organization-based RLS.
4. Replace mock portfolio values with database queries.
5. Connect weather and forecasting APIs.
6. Add MQTT/Modbus/OPC-UA ingestion through a backend/edge gateway.
7. Connect anomaly models and Virtual Energy Expert.
8. Point the existing landing page `/sign-in` CTA to the deployed application.

