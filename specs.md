# AgentHub Admin Panel Specification

## Product Overview

AgentHub is a platform for managing AI agents, their skills, and customer contracts. Its admin panel gives platform administrators one place to monitor activity, manage users and agents, browse skills, review contracts, and investigate execution errors.

The primary user is a platform administrator responsible for day-to-day operations. The interface should make platform health and revenue easy to scan and common management actions easy to reach.

## Technology and Constraints

- **Stack:** Use semantic HTML, Tailwind CSS through its CDN, and vanilla JavaScript. Do not add a framework, component library, build step, or backend.
- **Data and behavior:** Use representative hardcoded data. Navigation, menus, dialogs, theme switching, and row actions run in the browser only; do not add APIs, authentication, or database persistence.
- **Application shell:** Keep the six sections in one admin interface with persistent sidebar navigation, a shared top bar, and a clearly indicated active section.
- **Theme:** Provide light and dark themes. A top-bar control switches the complete interface, using Tailwind's `dark:` variant; retain the choice in the browser where practical.
- **Responsive behavior:** Make the sidebar, content, tables, and dialogs usable on narrow and wide screens. Tables may scroll horizontally or adapt their layout, but essential values and actions must remain reachable.
- **Tailwind vocabulary:** Use responsive variants such as `sm:`, `md:`, and `lg:`, layout utilities such as `grid`, `flex`, `gap-*`, and `overflow-x-auto`, and state utilities such as `dark:`, `hover:`, `focus-visible:`, and `disabled:` as useful. Treat these as a vocabulary of options, not a required class-by-class recipe; choose combinations that fit the content and preserve readable contrast.
- **Semantics and accessibility:** Use semantic HTML appropriate to the content and purpose of each control, without prescribing exact elements or markup patterns. Give controls accessible names, expose expanded/selected states, provide visible keyboard focus, and make dialogs dismissible with Escape where appropriate.

## Global Interface

1. **Application shell:** Provide persistent sidebar navigation for Dashboard, User Management, Agent Management, Skills, Agent Contracts, and Error Log. Keep it visible on wider screens; on small screens allow compact or collapsible navigation that remains easy to open. Mark the current destination accessibly and visually.
2. **Header and theme control:** Provide a shared top bar with the current view title and a clearly named light/dark toggle. Theme changes apply across the sidebar, content, tables, menus, and dialogs. Use responsive, focus, and `dark:` utilities as appropriate rather than prescribing exact class strings.
3. **Content and shared patterns:** Give each view a clear heading and semantic structure appropriate to its content. Reuse consistent status badges, action menus, and dialogs. Make controls keyboard reachable, show visible focus, close menus on outside click, and close dialogs with Escape or their close control.

## 1. Dashboard

1. **Nine-cell overview grid:** Use a responsive grid of nine dashboard tiles: on wide screens arrange three columns by three rows, reduce the column count as space narrows, and use one column on small screens. Include the four required KPIs (revenue this month, discount and coupon losses, active agents across clients, and failing agents), plus concise summaries for registered users, inactive agents, active contracts, and unresolved errors. Keep all values hardcoded and representative.
2. **Tile content and visual hierarchy:** Give each KPI or summary an icon, clear label, and prominent value. Use distinct but coordinated accents by metric type and subtle separation such as a border or shadow. Make the required four KPIs immediately scannable and maintain contrast in both themes. Tailwind grid, gap, padding, typography, border, shadow, and `dark:` utilities are suitable options, not fixed prescriptions.
3. **Activity tile:** Use the ninth tile for a weekly activity chart placeholder, with a dashed boundary and centered label. It must read as a reserved visualization rather than a rendered chart. On narrow screens the tile participates in the single-column flow; on wider screens it occupies one cell of the 3-by-3 grid so the overview remains a coherent nine-tile layout.

## 2. User Management

1. **User records and layout:** Present representative hardcoded users in a clearly labeled, scannable data layout with name, email, plan, status, and actions. Use semantic HTML appropriate to the records and readable status badges. On small screens, allow horizontal scrolling or use a compact layout without hiding values or actions.
2. **Row actions:** Give each user a clearly named compact action control that opens a menu with “View detail” and “Delete.” Associate the menu with that user, expose its open state accessibly, and close it after selection or an outside click. Use Tailwind layout, spacing, border, hover, and focus-visible utilities as useful, without locking the design to exact classes.
3. **Detail and deletion:** “View detail” opens a modal dialog containing the selected user's full record, with a close control and Escape dismissal. “Delete” requests confirmation and then removes the user from the in-memory displayed list only. Ensure the dialog fits narrow viewports, remains readable in both themes, and returns focus to its triggering control when closed.

## 3. Agent Management

1. **Agent records:** Present hardcoded agents in a clearly labeled data layout with agent name, owner, status, skills, and actions. Use semantic HTML appropriate to the records, and distinguish active, inactive, and failing states with readable text as well as color. On narrow screens, allow horizontal scrolling or adapt the layout while preserving all fields.
2. **Expandable skills:** Initially show a concise preview of each agent's associated skills and a button indicating when more are available. Activating it reveals the full list for that agent with a smooth, restrained transition; activating it again collapses the list. Reflect the state accessibly (for example, with `aria-expanded`) and keep the control usable on touch screens.
3. **Configuration and actions:** Each agent row has an action menu with “Configure” and “Delete.” “Configure” opens a responsive dialog showing that agent's system prompt in a readable, selectable text region. “Delete” requires confirmation and removes the agent from the in-memory list only. Use consistent menu and dialog patterns, visible keyboard focus, and light/dark styling.

## 4. Skills

1. **Catalog structure:** Present hardcoded skills in a clearly grouped catalog. Each entry includes a skill name, short description, enabled state, and a visible count of agents using it. Use a one-column flow on small screens and add columns as space permits; Tailwind grid, flex, and gap utilities are appropriate options.
2. **Context and visual states:** Include a concise explanation that a skill is a capability attachable to an agent. Make enabled/unused states understandable through text or a badge, not color alone. Let descriptions wrap naturally and keep the catalog readable in both themes using suitable text, border, spacing, and `dark:` utilities.
3. **Skill actions:** Give each entry an action button opening a menu with “View detail” and “Delete.” The detail dialog shows the full description and enablement information. Deletion requires confirmation and updates the local catalog only. Keep menus and dialogs keyboard accessible and sized to fit mobile viewports.

## 5. Agent Contracts

1. **Contracts and layout:** Present hardcoded active and past contracts in a clearly labeled data layout with client, rented agent, contracted skills, contract dates, total amount paid, and actions. Make status explicit. On narrow screens, allow horizontal scrolling or adapt the layout while preserving all fields.
2. **Contract breakdown:** Each contract's action menu offers “View detail.” Open a responsive dialog showing the full contract breakdown and an itemized list of contracted skills with an individual price for each. Use semantic structure appropriate to the line items and format dates and currency consistently.
3. **Interaction and readability:** Provide a close control and Escape dismissal, and ensure the dialog content can scroll on short screens without hiding its controls. Keep active/past labels and amounts understandable in light and dark themes; use responsive spacing and overflow utilities as needed rather than prescribing fixed dimensions.

## 6. Error Log

1. **Error records:** Present representative hardcoded errors in a clearly labeled data layout with timestamp, agent name, error type, short description, and actions. Use semantic HTML appropriate to the records. On narrow screens allow horizontal scrolling or adapt to compact records while keeping timestamps and row actions accessible.
2. **Severity and scanability:** Categorize errors by type or severity with color-coded badges that also include readable text. Include varied examples and enough spacing and contrast to distinguish entries in both themes. Use responsive Tailwind layout, typography, border, and `dark:` utilities as appropriate.
3. **Trace and resolution:** Each row's action menu offers “View detail” and “Mark as resolved.” The detail dialog shows the full error trace in a readable, scrollable region. “Mark as resolved” updates the in-memory entry and visibly labels it resolved without removing it. Menus and dialogs must remain keyboard accessible and usable on small screens.

## Reusable Component Inventory

Implement these as shared visual and behavioral patterns using the specified stack; this inventory describes their responsibilities, not a required component framework or file structure.

1. **Application sidebar:** Brand area, six section links, active-section indicator, and a compact/collapsible small-screen state.
2. **Top bar:** Current section title and shared theme toggle.
3. **Theme toggle:** One accessible control that switches the complete interface between light and dark themes and retains the choice where practical.
4. **Section heading:** Consistent title and optional short context for each view.
5. **Metric/summary tile:** Dashboard icon, label, value, and optional accent treatment; supports both required KPIs and secondary summaries.
6. **Data collection layout:** Shared visual treatment for user, agent, contract, and error records, with responsive overflow or compact presentation.
7. **Status/severity badge:** Reusable text-and-color indicator for user, agent, contract, skill, and error states.
8. **Action dropdown:** Row-associated menu trigger and menu items; supports outside-click dismissal and accessible expanded state.
9. **Modal dialog:** Shared overlay, title/content region, close control, Escape dismissal, and responsive sizing for user details, agent configuration, skill details, contract breakdowns, and error traces.
10. **Confirmation dialog:** Reusable confirmation step for destructive local actions such as deleting a user, agent, or skill.
11. **Collapsible skill preview:** Agent skill summary with expand/collapse control and an accessible expanded state.
12. **Chart placeholder:** Dashboard's weekly activity placeholder, visually distinct from functioning chart data.

## Acceptance Criteria

1. The interface contains all six sections, and selecting each sidebar destination displays the corresponding view and updates the active navigation indicator.
2. The dashboard displays a responsive 3-by-3 grid on wide screens, all four required KPI values, the four secondary summaries, and a weekly activity placeholder. The grid reflows at narrower widths without clipping content.
3. The user, agent, contract, and error views display the required fields from their specifications. On narrow screens, all fields and row actions remain reachable through responsive layout or horizontal scrolling.
4. Every row action dropdown opens for its associated record, exposes its expanded state, and closes after an action or an outside click.
5. User detail, agent configuration, skill detail, contract breakdown, and error trace dialogs display the selected record's information and can be closed using the close control or Escape.
6. Closing a dialog returns keyboard focus to the control that opened it, and keyboard users can reach all navigation and interactive controls with visible focus.
7. Agent skill previews start collapsed; activating a preview reveals the remaining skills, and activating it again collapses them while updating its accessible expanded state.
8. The theme toggle switches the entire interface, including dialogs, menus, and badges, between readable light and dark themes; the selected theme is retained where practical.
9. Deleting a user, agent, or skill requires confirmation and then updates only the displayed in-memory data; no backend or network request is used.
10. Marking an error as resolved updates its visible state without removing the error record.
11. The interface uses hardcoded representative data and runs with semantic HTML, Tailwind CSS from its CDN, and vanilla JavaScript only; it has no framework, build step, API, or backend dependency.