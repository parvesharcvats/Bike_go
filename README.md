# Bike_go
from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, PageBreak, Table, TableStyle, KeepTogether
from reportlab.lib import colors
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.enums import TA_CENTER
from reportlab.lib.units import mm
from reportlab.pdfbase.ttfonts import TTFont
from reportlab.pdfbase import pdfmetrics
import os

out = "/mnt/data/BikeGo_Project_Report.pdf"

doc = SimpleDocTemplate(
    out, pagesize=A4, rightMargin=20*mm, leftMargin=20*mm,
    topMargin=18*mm, bottomMargin=18*mm,
    title="BikeGo - AI-Powered Bike Taxi & Local Mobility Platform",
    author="BikeGo Project"
)

styles = getSampleStyleSheet()
styles.add(ParagraphStyle(name="CoverTitle", parent=styles["Title"], fontName="Helvetica-Bold",
                          fontSize=30, leading=36, textColor=colors.HexColor("#153B50"),
                          alignment=TA_CENTER, spaceAfter=14))
styles.add(ParagraphStyle(name="CoverSub", parent=styles["Normal"], fontName="Helvetica",
                          fontSize=13, leading=19, textColor=colors.HexColor("#43616F"),
                          alignment=TA_CENTER, spaceAfter=10))
styles.add(ParagraphStyle(name="H1x", parent=styles["Heading1"], fontName="Helvetica-Bold",
                          fontSize=18, leading=23, textColor=colors.HexColor("#153B50"),
                          spaceBefore=8, spaceAfter=10))
styles.add(ParagraphStyle(name="H2x", parent=styles["Heading2"], fontName="Helvetica-Bold",
                          fontSize=12, leading=16, textColor=colors.HexColor("#167D8D"),
                          spaceBefore=7, spaceAfter=5))
styles.add(ParagraphStyle(name="Bodyx", parent=styles["BodyText"], fontName="Helvetica",
                          fontSize=9.5, leading=14, spaceAfter=7))
styles.add(ParagraphStyle(name="Smallx", parent=styles["BodyText"], fontName="Helvetica",
                          fontSize=8, leading=11, textColor=colors.HexColor("#53636A"), spaceAfter=4))
styles.add(ParagraphStyle(name="Codex", parent=styles["Code"], fontName="Courier",
                          fontSize=8, leading=11, leftIndent=8, rightIndent=8,
                          backColor=colors.HexColor("#F2F6F7"), borderPadding=7, spaceAfter=8))

story = []
P = lambda txt, sty="Bodyx": Paragraph(txt, styles[sty])

# Cover
story += [Spacer(1, 28*mm), P("BikeGo", "CoverTitle"),
          P("AI-Powered Bike Taxi &amp; Local Mobility Platform", "CoverSub"),
          Spacer(1, 5*mm),
          P("Project Report &amp; GitHub Documentation", "CoverSub"),
          Spacer(1, 20*mm)]
cover_table = Table([
    [P("<b>Project type</b>", "Bodyx"), P("Smart mobility / transport technology", "Bodyx")],
    [P("<b>Core idea</b>", "Bodyx"), P("Connect passengers with nearby bike-taxi riders using intelligent matching and transparent fares.", "Bodyx")],
    [P("<b>Primary users</b>", "Bodyx"), P("Passengers, riders, and platform administrators", "Bodyx")],
    [P("<b>Project status</b>", "Bodyx"), P("Concept and proposed system design", "Bodyx")],
], colWidths=[38*mm, 105*mm])
cover_table.setStyle(TableStyle([
    ("BACKGROUND", (0,0), (0,-1), colors.HexColor("#E8F2F4")),
    ("BOX", (0,0), (-1,-1), 0.6, colors.HexColor("#C5D6DB")),
    ("INNERGRID", (0,0), (-1,-1), 0.4, colors.HexColor("#D7E2E5")),
    ("VALIGN", (0,0), (-1,-1), "TOP"),
    ("LEFTPADDING", (0,0), (-1,-1), 9),
    ("RIGHTPADDING", (0,0), (-1,-1), 9),
    ("TOPPADDING", (0,0), (-1,-1), 8),
    ("BOTTOMPADDING", (0,0), (-1,-1), 5),
]))
story += [cover_table, Spacer(1, 24*mm),
          P("Prepared as a starter project document. Replace proposed features, technology choices, and implementation status with verified details as the software develops.", "Smallx"),
          PageBreak()]

# Contents
story += [P("Contents", "H1x")]
contents = [
    "1. Executive Summary", "2. Problem Statement", "3. Goals and Scope",
    "4. Proposed Features", "5. User Roles and User Journey", "6. AI and Intelligent Mobility",
    "7. System Architecture", "8. Suggested Technology Stack", "9. Data Model",
    "10. Safety, Privacy and Security", "11. API Design (Proposal)", "12. Development Roadmap",
    "13. Testing and Success Metrics", "14. Risks and Mitigations", "15. Future Enhancements",
    "16. GitHub Repository Structure", "17. Conclusion", "Appendix: README Starter"
]
for c in contents:
    story.append(P(c))
story.append(PageBreak())

sections = [
("1. Executive Summary", [
("body", "BikeGo is a proposed AI-powered bike-taxi and local mobility platform intended to make short-distance urban travel faster, affordable, and convenient. The platform connects passengers who need a ride with available nearby riders, provides estimated fares and arrival times, and supports trip tracking and digital trip records."),
("body", "The system is designed around three interfaces: a passenger application, a rider application, and an administrative dashboard. Intelligent features may help rank nearby riders, estimate trip duration, forecast demand, and detect unusual trip patterns. These capabilities are design goals, not claims that a working AI model has already been trained or deployed."),
("body", "<b>Important:</b> this document describes a concept and proposed architecture. Actual features, integrations, compliance, and implementation status should be updated to match the repository.")
]),
("2. Problem Statement", [
("body", "People making short trips may face traffic congestion, uncertain fares, difficulty finding transport quickly, and limited visibility into a trip once it begins. Riders can face uneven demand and wasted time waiting between bookings."),
("body", "BikeGo proposes a digital workflow that shows an estimated fare before booking, matches a passenger with an available rider, shares trip status, and records completed journeys. The platform should prioritize safety, transparency, accessibility, and responsible handling of location data.")
]),
("3. Goals and Scope", [
("h2", "Objectives"),
("bullet", "Reduce friction in booking short-distance rides."),
("bullet", "Show an estimated fare and arrival time before confirmation."),
("bullet", "Help riders discover nearby trip requests and manage availability."),
("bullet", "Provide trip status, receipts, feedback, and support workflows."),
("bullet", "Use data-driven tools to improve matching and demand planning over time."),
("h2", "Initial scope"),
("body", "The minimum viable product (MVP) can include account registration, pickup/drop-off selection, fare estimation, ride requests, rider acceptance, trip status updates, and trip history. Live maps, payment gateways, identity verification, emergency workflows, and AI-based prediction require suitable providers, testing, and operational policies."),
("h2", "Out of scope for the initial prototype"),
("body", "A production-grade dispatch network, guaranteed arrival times, real-time fraud detection, autonomous vehicles, and availability in every city are not assumed.")
]),
("4. Proposed Features", [
("h2", "Passenger application"),
("bullet", "Sign up and manage a profile."),
("bullet", "Choose pickup and destination on a map or by address."),
("bullet", "View estimated distance, fare range, and rider arrival estimate."),
("bullet", "Request, cancel where permitted, and follow ride status."),
("bullet", "View trip history, receipts, ratings, and support options."),
("h2", "Rider application"),
("bullet", "Manage profile and availability status."),
("bullet", "Receive nearby ride requests with pickup and destination details appropriate to the workflow."),
("bullet", "Accept or decline requests and update trip progress."),
("bullet", "Review completed trips and earnings summaries."),
("h2", "Admin dashboard"),
("bullet", "Review user reports and support cases."),
("bullet", "Manage rider onboarding and account status."),
("bullet", "Monitor aggregate trip, cancellation, and service-quality metrics."),
("bullet", "Apply documented access controls and audit sensitive actions.")
]),
("5. User Roles and User Journey", [
("h2", "Roles"),
("body", "<b>Passenger:</b> requests and tracks trips. <b>Rider:</b> receives and completes accepted trips. <b>Administrator/support agent:</b> handles onboarding, reports, disputes, and platform operations."),
("h2", "Example passenger journey"),
("body", "1) Open BikeGo and set pickup/drop-off. 2) Review estimated fare and ride details. 3) Confirm the request. 4) View matching and rider assignment status. 5) Verify rider and vehicle details before boarding. 6) Follow the trip status. 7) Complete the trip, pay through an enabled method, and submit feedback."),
("h2", "Suggested ride states"),
("body", "REQUESTED → MATCHING → ACCEPTED → RIDER_ARRIVING → IN_PROGRESS → COMPLETED. Alternative states include CANCELLED, EXPIRED, and SUPPORT_REVIEW. State changes should be validated by the backend rather than trusted solely from the mobile client.")
]),
("6. AI and Intelligent Mobility", [
("body", "AI should support decisions, not make opaque or unsafe decisions without oversight. Start with explainable rules and introduce machine-learning models only when representative, consented, and appropriately governed data is available."),
("h2", "Potential AI use cases"),
("bullet", "<b>Rider matching:</b> rank eligible riders by estimated pickup time, distance, availability, and service constraints."),
("bullet", "<b>ETA estimation:</b> combine map-provider estimates with historical trip durations when data quality is sufficient."),
("bullet", "<b>Demand forecasting:</b> estimate busy zones and time windows from aggregated historical bookings."),
("bullet", "<b>Fare guidance:</b> estimate trip cost using distance, time, local rules, and clearly disclosed pricing logic."),
("bullet", "<b>Anomaly flags:</b> identify unusual patterns for human review; avoid automatically penalizing users based only on a model score."),
("h2", "Example matching score (illustrative)"),
("code", "score = 0.50 × normalized_pickup_time\\n      + 0.25 × normalized_distance\\n      + 0.15 × rider_reliability\\n      + 0.10 × vehicle_eligibility"),
("body", "This formula is a placeholder for a prototype, not a validated production model. Weights must be tested for fairness, safety, and local operating conditions. Do not use protected traits or sensitive personal data for ranking.")
]),
("7. System Architecture", [
("body", "A practical architecture separates client interfaces, backend business rules, data storage, and external providers. The backend should remain the authority for booking state, fare rules, permissions, and trip history."),
("h2", "Logical components"),
("bullet", "<b>Passenger app / web client:</b> booking, fare preview, trip status, history."),
("bullet", "<b>Rider app:</b> availability, request handling, navigation handoff, trip updates."),
("bullet", "<b>API backend:</b> authentication, ride lifecycle, matching, fare calculation, notifications."),
("bullet", "<b>Database:</b> users, rider profiles, rides, payments references, ratings, support cases."),
("bullet", "<b>External services:</b> maps/geocoding, push notifications, payment gateway, optional SMS/email."),
("bullet", "<b>Analytics/AI service:</b> aggregate metrics and separately evaluated prediction services.")
]),
("8. Suggested Technology Stack", [
("body", "Choose tools based on team experience and deployment needs. This is one possible stack, not a requirement."),
("bullet", "<b>Mobile:</b> Flutter or React Native for cross-platform development."),
("bullet", "<b>Web/admin:</b> React with TypeScript."),
("bullet", "<b>Backend:</b> Node.js with Express/NestJS, or Python with FastAPI."),
("bullet", "<b>Database:</b> PostgreSQL; consider PostGIS for geographic queries."),
("bullet", "<b>Maps:</b> a licensed maps/geocoding/directions provider."),
("bullet", "<b>Authentication:</b> managed identity provider or secure server-side authentication."),
("bullet", "<b>Deployment:</b> a cloud platform with secret management, logging, monitoring, and backups."),
("body", "Never commit API keys, signing credentials, database passwords, real user location histories, or payment secrets to GitHub. Use environment variables and a committed .env.example containing placeholders only.")
]),
("9. Data Model", [
("body", "The following entities are a starting point. Use generated IDs, timestamps, validation, and appropriate access rules."),
("h2", "Core entities"),
("bullet", "<b>User:</b> id, display_name, contact_reference, role, account_status, created_at."),
("bullet", "<b>RiderProfile:</b> user_id, verification_status, vehicle_type, vehicle_registration_reference, availability_status."),
("bullet", "<b>Ride:</b> id, passenger_id, rider_id, pickup coordinates/reference, destination coordinates/reference, estimated_fare, final_fare, status, created_at, completed_at."),
("bullet", "<b>RideEvent:</b> id, ride_id, event_type, timestamp, actor_id."),
("bullet", "<b>PaymentRecord:</b> id, ride_id, provider_reference, amount, currency, status; do not store raw card data."),
("bullet", "<b>Rating:</b> id, ride_id, reviewer_id, score, optional_comment, created_at."),
("body", "Minimize collection of precise location data, restrict who can access it, define retention periods, and avoid putting live user records in demo datasets.")
]),
("10. Safety, Privacy and Security", [
("bullet", "Use encrypted transport (HTTPS/TLS) and secure credential storage."),
("bullet", "Apply role-based authorization on every sensitive backend endpoint."),
("bullet", "Collect only data needed for the ride and service operation."),
("bullet", "Explain location permissions and request them only when needed."),
("bullet", "Use verified rider/vehicle workflows appropriate to the operating jurisdiction."),
("bullet", "Provide a clear emergency/support process and escalation ownership before launch."),
("bullet", "Keep audit records for administrative actions and protect them from tampering."),
("bullet", "Rate-limit authentication and booking endpoints; validate all user input."),
("bullet", "Use payment providers; do not store raw card details."),
("bullet", "Test for common web/mobile security issues and have an incident response plan."),
("body", "A real bike-taxi service must assess applicable transport, licensing, insurance, consumer-protection, tax, accessibility, and data-protection requirements for each location. This report is not legal advice and does not claim that BikeGo is approved to operate.")
]),
("11. API Design (Proposal)", [
("body", "Example REST endpoints for a future backend. These are illustrative contracts and do not imply that endpoints currently exist."),
("code", "POST   /api/v1/auth/register\\nPOST   /api/v1/auth/login\\nGET    /api/v1/users/me\\nPOST   /api/v1/rides/estimate\\nPOST   /api/v1/rides\\nGET    /api/v1/rides/{rideId}\\nPOST   /api/v1/rides/{rideId}/accept\\nPOST   /api/v1/rides/{rideId}/events\\nPOST   /api/v1/rides/{rideId}/cancel\\nGET    /api/v1/users/me/rides"),
("body", "Require authentication where appropriate, validate ownership and role, use idempotency for booking/payment operations, and return consistent error codes. Do not expose another user's private trip information.")
]),
("12. Development Roadmap", [
("h2", "Phase 1 — Prototype"),
("bullet", "Create wireframes, user stories, and a basic responsive interface."),
("bullet", "Implement sample ride booking and state transitions with mock data."),
("bullet", "Write setup instructions, tests, and API documentation."),
("h2", "Phase 2 — MVP"),
("bullet", "Add real authentication, persistent database, role-based access, and validated fare estimates."),
("bullet", "Integrate maps and notifications after provider selection and configuration."),
("bullet", "Add rider onboarding, support workflows, and trip receipts."),
("h2", "Phase 3 — Pilot"),
("bullet", "Run a limited, supervised pilot after legal, safety, insurance, and operational checks."),
("bullet", "Measure matching performance, trip completion, cancellations, and user feedback."),
("h2", "Phase 4 — Intelligence and scale"),
("bullet", "Evaluate demand forecasting and ETA models using quality-controlled data."),
("bullet", "Monitor model drift, fairness, security, costs, and reliability.")
]),
("13. Testing and Success Metrics", [
("h2", "Testing checklist"),
("bullet", "Unit tests for fare calculation, permissions, and ride-state transitions."),
("bullet", "Integration tests for booking, rider acceptance, cancellation, and trip completion."),
("bullet", "Authorization tests proving passengers cannot access unrelated rides."),
("bullet", "Failure tests for network loss, duplicate requests, payment errors, and unavailable riders."),
("bullet", "Accessibility, usability, performance, and security testing before deployment."),
("h2", "Possible metrics"),
("body", "Median time to rider assignment; pickup ETA error; booking completion rate; cancellation rate; ride completion rate; crash/error rate; support resolution time; passenger and rider satisfaction; and safety incidents. Define measurement windows and baselines before interpreting results.")
]),
("14. Risks and Mitigations", [
("bullet", "<b>Incorrect ETA or fare:</b> show estimates clearly, explain fare rules, and monitor error ranges."),
("bullet", "<b>Insufficient rider supply:</b> display availability honestly and avoid promising guaranteed matches."),
("bullet", "<b>Location-data exposure:</b> minimize retention, enforce access controls, and audit access."),
("bullet", "<b>Unsafe or fraudulent activity:</b> verification, reporting, human review, and clear escalation procedures."),
("bullet", "<b>Biased AI recommendations:</b> test across relevant areas and groups; provide appeal and human review."),
("bullet", "<b>Provider outage:</b> define graceful failure states and fallback procedures."),
("bullet", "<b>Regulatory uncertainty:</b> complete location-specific review before any real-world launch.")
]),
("15. Future Enhancements", [
("bullet", "Multilingual UI and accessible design."),
("bullet", "Scheduled rides and multi-stop trip support."),
("bullet", "Demand heatmaps based on aggregated, privacy-preserving data."),
("bullet", "Transparent rider incentives and peak-time planning."),
("bullet", "Digital receipts, coupons, and business travel accounts."),
("bullet", "Public transport connections and other local mobility options."),
("bullet", "Model monitoring dashboard and human review queue.")
]),
("16. GitHub Repository Structure", [
("body", "A clean repository can separate application code, documentation, tests, and deployment configuration. Adapt this structure to the framework actually used."),
("code", "BikeGo/\\n├── README.md\\n├── LICENSE\\n├── .gitignore\\n├── .env.example\\n├── docs/\\n│   ├── BikeGo_Project_Report.pdf\\n│   ├── architecture.md\\n│   └── api.md\\n├── apps/\\n│   ├── passenger-app/\\n│   ├── rider-app/\\n│   └── admin-dashboard/\\n├── services/\\n│   ├── api/\\n│   └── matching/\\n├── tests/\\n└── assets/"),
("body", "Do not create empty folders just to match this diagram. Keep only the folders that correspond to real work, and update the README with actual setup commands and implemented features.")
]),
("17. Conclusion", [
("body", "BikeGo outlines a practical direction for a bike-taxi and local mobility platform: convenient booking, transparent estimates, rider matching, trip visibility, and a foundation for data-informed improvements. The safest path is to build a small, testable prototype first, document what works, and add production integrations only after reliability, privacy, safety, and local operating requirements have been addressed."),
("body", "This report is intended as project documentation for a GitHub repository. It should be revised as the implementation evolves so that planned features are clearly distinguished from completed functionality.")
]),
("Appendix: README Starter", [
("body", "Copy and a
The document clearly identifies BikeGo as a proposed project design. It does not falsely claim that Al models, payment integrations, or live ride-booking services are already implemented
