
tags: [workflow, template, spec, intake, ai-powered, stable] updated: 2026-06-16
Design Spec Auto-Intake Workflow
One-line trigger for AI agents. User provides a design source (website URL, designer name, etc.), and the AI agent automatically:

Fetches/researches the design source
Extracts all relevant design data
Fills out the intake form
Generates design-spec.json
Outputs a ready-to-use implementation prompt
No manual form-filling required.

How It Works: The User Trigger
User says any of these:

"Build a website in the style of www.jdsports.com"
"Create a page inspired by Stripe's pricing page"
"Make a landing page like Airbnb"
"Design a dashboard similar to Notion"
"I want the aesthetic of Apple's product pages"
That's it. The AI agent does the rest.

AI Agent Workflow (Auto-Execution)
Step 1: Parse User Intent
Extract:

Source type: website-url | designer-name | company-name | design-system
Source identifier: www.jdsports.com or Stripe or @designer-handle
Step 2: Research & Extract Design Data
Use web search (Bing) or known design patterns to gather:

Visual hierarchy at mobile (375px) and desktop (1440px)
Color palette (primary, secondary, accents, backgrounds, text)
Typography (headings, body, captions with sizes/weights)
Spacing scale (padding, margins, gaps)
Component library (buttons, cards, inputs, etc.)
Interactive states (hover, focus, active)
Animations (fade-ins, transitions, parallax if present)
Accessibility markers (semantic HTML, contrast, focus states)
Tools available:

bing-search — fetch live website data, screenshots, design reviews
semantic-code-search / lexical-code-search — if searching existing codebase
Public design documentation (Figma files, design systems, open-source code)
Step 3: Fill Out the Intake Form (Internally)
Map extracted data into a structured intake format with sections for colors, typography, spacing, layout, interactions, animations.

Step 4: Generate design-spec.json
Output a normalized JSON file with all extracted tokens and layout specs.

Step 5: Output Ready-to-Use Implementation Prompt
Generate a customized generic-layout-prompt variant that references:

The extracted design source
The filled design-spec.json
Ready for handoff to implementation
AI Agent Implementation Checklist
When a user triggers the workflow with a design source, follow this:

 Parse user's design source input
 Search for design data (web search, visual inspection, design docs)
 Extract colors, typography, spacing, layout, interactions, animations
 Map extracted data to intake form (internally, don't show user)
 Generate design-spec.json with all normalized tokens
 Output customized implementation prompt referencing the JSON
 Confirm with user: "I've analyzed [source]. Here's the spec. Ready to build?"
Template: Auto-Generated design-spec.json
When generating the JSON, use this structure:

JSON
{
  "metadata": {
    "project": "[PAGE_NAME]",
    "source": "[www.example.com | Designer Name | Company]",
    "sourceUrl": "[Link to original]",
    "analysisMethod": "web-search | visual-inspection | design-system-doc",
    "lastUpdated": "[ISO 8601 timestamp]",
    "notes": "[Key observations, assumptions, or caveats]"
  },
  "breakpoints": {
    "mobile": {
      "width": 375,
      "description": "[Key mobile layout features]"
    },
    "tablet": {
      "width": 768,
      "description": "[Tablet layout, or null]"
    },
    "desktop": {
      "width": 1440,
      "description": "[Key desktop layout features]"
    }
  },
  "tokens": {
    "colors": {
      "primary": "#[hex]",
      "secondary": "#[hex]",
      "background": "#[hex]",
      "text": "#[hex]"
    },
    "typography": {
      "h1": {
        "fontSize": "[px]",
        "fontWeight": "[number]",
        "lineHeight": "[decimal]"
      }
    },
    "spacing": {
      "base": "[unit]",
      "2x": "[unit]"
    }
  },
  "layout": {
    "mobile": {
      "sections": [
        {
          "name": "[Section]",
          "layout": "[vertical-stack | grid]",
          "elements": ["[Element]"]
        }
      ]
    },
    "desktop": {
      "sections": [
        {
          "name": "[Section]",
          "layout": "[grid-3-col]",
          "elements": ["[Element]"]
        }
      ]
    }
  },
  "interactions": {
    "buttons": {
      "default": { "bg": "[token]" },
      "hover": { "bg": "[token]" }
    }
  },
  "animations": [
    {
      "name": "[Animation]",
      "trigger": "[scroll | hover]",
      "duration": "[ms]"
    }
  ],
  "accessibility": {
    "semanticHtml": true,
    "contrastLevel": "WCAG AA"
  }
}
Example Flow: User Triggers "Build in the style of JD Sports"
User says:
"Build a website in the style of www.jdsports.com"

AI agent auto-executes:
Searches www.jdsports.com — fetches live site data
Extracts design data: colors, typography, layout
Generates design-spec.json with all tokens
Outputs ready-to-use prompt: "I've analyzed JD Sports. Ready to implement?"
User approves:
"Yes, build it"

AI builds:
Uses the JSON spec to stay on-brand
Creates responsive components
Implements all animations
Key Benefits
Manual Intake	Auto-Intake
User fills form	AI searches & extracts
15-30 min per page	Seconds
Error-prone	Comprehensive
Files Involved
This file (design-spec-auto-intake.md) — workflow documentation
design-spec.json — auto-generated output
generic-layout-prompt.md — implementation prompt
User never manually fills a form.