# Project Frontend Documentation: Campus Events Hub

This document provides a deep, detailed overview of the frontend architecture, design system, and user interface components of the **Campus Events Hub** project.

---

## 1. Frontend Technology Stack
The project uses a modern, clean, and lightweight frontend stack without heavy frameworks, prioritizing performance and maintainability.

- **Templating**: Django Template Language (DTL) with a hierarchical inheritance structure.
- **Styling**: Vanilla CSS3 using CSS Variables for a robust design system. No external CSS frameworks (like Bootstrap or Tailwind) are used, allowing for a custom, premium aesthetic.
- **Interactivity**: Pure JavaScript (ES6+) for dynamic behaviors and the `Fetch API` for AJAX communications.
- **External Integrations**: 
  - **Razorpay SDK**: For secure payment processing.
  - **Google Fonts**: 'Segoe UI' and system-ui fallbacks.

---

## 2. Design System & Aesthetics
The project follows a **"Clean Modern"** aesthetic with a curated color palette and consistent spacing.

### Color Palette (Defined via CSS Variables)
| Color | Variable | Hex Code | Usage |
| :--- | :--- | :--- | :--- |
| **Purple** | `--purple` | `#534AB7` | Primary Brand, Student Theme |
| **Teal** | `--teal` | `#1D9E75` | Success, Organizer Theme |
| **Amber** | `--amber` | `#BA7517` | Warnings, Sports Category |
| **Pink** | `--pink` | `#D4537E` | Secondary Accents, Cultural Category |
| **Red** | `--red` | `#E24B4A` | Errors, Danger Actions |
| **Gray** | `--gray` | `#888780` | Muted Text, Borders |
| **BG** | `--bg` | `#F8F8F6` | Global Background |

### Design Tokens
- **Radius**: `8px` (Standard), `12px` (Large cards).
- **Shadows**: Subtle shadows (`0 1px 3px rgba(0,0,0,0.08)`) for depth.
- **Typography**: Focused on readability with `15px` base font and `13px` for secondary data.

---

## 3. Template Architecture
The project uses a multi-level inheritance pattern to minimize code duplication.

### Hierarchy
1.  **`base.html`**: The root skeleton (HTML5 boilerplate, global fonts, `base.css` link).
2.  **Role-Specific Bases**:
    *   `base_student.html`: Defines the student sidebar, topbar, and notifications.
    *   `base_organizer.html`: Defines the organizer-specific navigation.
3.  **Feature Templates**: Specific pages (e.g., `dashboard.html`, `create_event.html`) that fill the role-specific content blocks.

---

## 4. Core UI Components

### 4.1 Layout Components
- **Sidebar**: A fixed left-hand navigation bar with role-specific links, icons (emojis), and user profile snippets.
- **Topbar**: A sticky header showing the app brand, current role, and user identity.
- **Main Content Area**: A flexible container with standard padding (`1.5rem`) for all page content.

### 4.2 UI Elements
- **Cards (`.card`)**: White background, rounded corners, and subtle borders. Used for grouping related data.
- **Badges (`.badge`)**: Color-coded labels for statuses (`Pending`, `Active`, `Completed`) and event categories (`Technical`, `Cultural`).
- **Stat Cards (`.stat-card`)**: High-visibility components for dashboards showing key metrics (e.g., Total Revenue, Registrations).
- **Buttons (`.btn`)**: Rounded buttons with hover transitions. Variants: `primary`, `success`, `warning`, `danger`, `outline`.
- **Forms (`.form-control`)**: Clean, minimalist inputs with focus effects using the brand purple.

---

## 5. Role-Specific Dashboards

### 5.1 Student Panel
- **Event Discovery**: A grid-based view of available events with filtering capabilities.
- **Registration Flow**: Multi-step process (Selection -> Team Management -> Payment/Confirmation).
- **Team Management**: Real-time interface to invite members, revoke invites, and see team status (integrated with `team.css`).
- **Certificates**: A dedicated gallery for participation and winner certificates.

### 5.2 Organizer Panel
- **Event Lifecycle**: Forms for creating Mega Events and Sub-Events with date/time pickers.
- **Volunteer Hub**: Management system for tracking volunteer applications and assignments.
- **Analytics**: Visual summary of event performance, registration counts, and revenue tracking.
- **Gallery Manage**: Interface for uploading and managing event photos/videos.

---

## 6. Interactive Features & Logic

### 6.1 Razorpay Payment Flow
Integrated directly into the `payment_page.html`.
- **Flow**:
  1. User clicks "Pay".
  2. JavaScript initiates the Razorpay modal.
  3. On success, `fetch()` sends the `payment_id` and `signature` to the Django backend for verification.
  4. The page redirects based on the JSON response from the server.

### 6.2 Team Management Logic
- Uses dynamic status updates.
- Female member requirement validation is performed on the frontend (showing warnings) before allowing payment/registration.

### 6.3 Notification System
Uses Django's `messages` framework.
- Alerts are color-coded (Success = Teal, Error = Red).
- Includes an `auto-dismiss` behavior (implemented via CSS or simple JS) to keep the UI clean.

---

## 7. Static Asset Structure
```text
static/
├── css/
│   ├── base.css           # Global design system
│   ├── landing/           # Landing page specific styles
│   ├── student/           # Student-only styles (e.g., team.css)
│   └── accounts/          # Login/Register page styles
├── img/                   # Icons, logos, and default posters
└── js/                    # Global JS utilities (if any)
```

---

## 8. Responsive Design
The project uses a mobile-first approach for many components:
- **Grids**: Use `grid-template-columns: repeat(auto-fill, ...)` to adapt to screen width.
- **Flexbox**: Used for topbars and footers to ensure elements wrap or align correctly on small screens.
- **Sidebar**: Designed to be the primary anchor, often hidden or collapsed on mobile (depending on implementation specifics).
