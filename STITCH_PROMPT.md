# Prompt para Google Stitch

Copia el prompt siguiente en Google Stitch para generar la propuesta visual de AgentHub. Pide las seis vistas como pantallas del mismo producto y conserva el mismo sistema visual en todas.

## Prompt

Design a polished, high-fidelity responsive web app for **AgentHub**, an admin workspace for managing AI agents, their skills, integrations, and activity. The audience is a workspace administrator who needs to scan operational status quickly and make routine changes confidently. This is a practical product UI, not a marketing landing page.

### Screens

Create six connected screens that share one application shell and consistent navigation:

1. **Dashboard:** four metric tiles in a 2x2 desktop grid: Total agents 12, Active agents 8, Runs this week 1,284, Success rate 98.6%. Each tile has an icon, label, hardcoded value, distinct restrained accent, and a text trend versus the previous period. Add a seven-day weekly activity bar chart with visible day labels and values, plus a compact list of three recently used agents with status and last run.
2. **Agents:** a scannable table with at least four sample agents, columns for name, description, status, assigned skills, last run, and row actions. Include name search, status filter, a prominent but restrained New agent action, and an example row-actions dropdown.
3. **Skills:** a categorized skills catalog with collapsible category headers, skill name and summary, usage count, availability badge, and a clear selected-skill detail panel showing assigned agents.
4. **Integrations:** a directory of at least four fictional integrations with purpose, connected/not connected status, and contextual Connect, Disconnect, or Configure actions. Show one configuration dialog state.
5. **Activity:** a recent-first event log with timestamp, actor, action, resource, and result columns; include search, event-type and result filters, plus an example event-detail dialog.
6. **Settings:** a compact workspace profile form, notification toggles, a light/dark theme toggle, and a separated Reset demo data action with a confirmation dialog state.

### Shared visual system

- Use a persistent left sidebar on desktop with the AgentHub wordmark and exactly these navigation items: Dashboard, Agents, Skills, Integrations, Activity, Settings. Clearly indicate the active item. On mobile, convert it into a compact collapsible navigation drawer.
- Use an operational, information-dense layout: compact page titles, clear section hierarchy, aligned data columns, subtle separators, and restrained surfaces. Avoid oversized hero headings, marketing sections, nested cards, excessive pill shapes, and decorative gradients.
- Establish a crisp light theme with white and cool light-gray surfaces, dark graphite text, and balanced cobalt, teal, amber, and coral accents. Reserve colors for chart series, metric distinctions, actions, and statuses; do not rely on color alone to communicate status. Also show a coherent dark-theme variant.
- Use a distinctive readable sans-serif for interface text and a restrained monospaced style for numeric details. Keep typography compact and legible, with no viewport-scaled text.
- Use compact cards with subtle borders and square-to-small corner radii. Keep content aligned to a consistent grid and leave enough whitespace for scanning without making the dashboard sparse.
- Show realistic fictional data, useful empty/filter states, visible keyboard focus, and accessible labels. Use icons consistently for navigation and actions.
- Create desktop views at approximately 1440px wide and mobile adaptations at approximately 390px wide. Tables should remain usable on narrow screens without page-level horizontal overflow.

### Interaction states to visualize

- An open row-actions dropdown on Agents.
- An open confirmation or edit modal with clear primary and secondary actions.
- An expanded and a collapsed Skills category.
- Connected and disconnected integration rows.
- The Dashboard in both light and dark themes.
- Responsive sidebar navigation on mobile.

Keep the result faithful to this admin workflow and visually consistent across all six screens. Do not invent authentication, billing, external integrations that actually connect, or backend functionality; all displayed data represents a local demo prototype.