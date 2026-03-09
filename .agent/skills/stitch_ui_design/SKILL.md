---
name: Stitch UI Design
description: A skill to autonomously generate UI designs from Product Requirements Documents (PRD) using the Stitch MCP.
---

# Stitch UI Design Skill

This skill allows the agent to read existing product design specifications within the workspace and translate them into high-fidelity UI code using the Stitch MCP integration.

## Prerequisites
- A PRD document must exist in the workspace, typically under `产品设计/初步产品设计_PRD.md` or a similar path.
- The `mcp_StitchMCP_create_project` and `mcp_StitchMCP_generate_screen_from_text` tools must be available.

## Steps to Execute
1. **Locate Design Context**: Find and read the PRD markdown file (e.g., `初步产品设计_PRD.md`) and any interaction flows in the `产品设计/` directory.
2. **Create Project**: Call the `mcp_StitchMCP_create_project` tool with a relevant title matching the PRD's product name. Note the returned `projectId`.
3. **Generate UI Screen**: 
   - Construct a highly detailed prompt containing:
     - The core functional requirements extracted from the PRD.
     - The desired aesthetic qualities (e.g., modern SaaS, minimalist, specific color palettes like Slate/Indigo).
     - Component layout hierarchy (Sidebar, Header, Main Content Area).
   - Call `mcp_StitchMCP_generate_screen_from_text`, passing in the `projectId`, `deviceType` (usually `DESKTOP` or `MOBILE`), the `modelId` (e.g., `GEMINI_3_PRO`), and the constructed `prompt`.
4. **Download Assets (Optional)**: If the prompt returns download URLs for the HTML code and screenshots, use `curl` to download them into the `UI设计/` directory for the user to review locally.
5. **Present to User**: Notify the user that the UI has been generated, providing links to the live preview URLs, downloaded files, and offering any follow-up suggestions returned by the Stitch MCP (like adjusting the dark mode or adding animations).

## Best Practices
- **Do not invent features**: Only pass what is explicitly written in the PRD.
- **Set the tone**: Always enforce high-quality, modern, and clean UI design tokens in the prompt. Do not settle for generic colors; specify modern palettes (e.g., Zinc, Slate, Indigo, Emerald).
- **Component breakdown**: If the application is large, generate screens component-by-component or page-by-page rather than attempting to generate the entire platform in one prompt.
