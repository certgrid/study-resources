# 03 - Demonstrate the Capabilities of Power Apps

This domain is worth 20-25% of the exam. It tests whether you can pick the right Power Apps experience for a scenario (canvas app, model-driven app, Plan designer, or code apps) and describe how AI helps you build apps: generating canvas and model-driven apps with Copilot and iterating with the vibe experience.

## Mental model

Power Apps offers different ways to get an app, sorted by how much control vs speed you want. Canvas apps start from a blank screen and give you pixel control. Model-driven apps start from Dataverse data and generate the UI for you. Plan designer starts from a business problem and lets AI propose the whole solution. Code apps let professional developers bring real code into the platform. Copilot and the vibe experience are the AI accelerators across all of it.

| Scenario keyword                                               | Likely concept              |
| -------------------------------------------------------------- | --------------------------- |
| Pixel-perfect design, start from a blank screen                | Canvas app                  |
| UI generated from Dataverse tables, forms, and views           | Model-driven app            |
| Describe a business problem, AI proposes tables, apps, agents  | Plan designer               |
| Professional developers bring custom code apps to the platform | Code apps                   |
| "Create an app from this description or data"                  | Copilot / AI app generation |
| Chat back and forth with AI to refine a generated app          | Vibe experience             |
| Excel-like formulas in an app                                  | Power Fx                    |

## Canvas apps

Canvas apps are design-first. The maker drags controls (galleries, forms, buttons, labels) onto screens and wires up behavior with Power Fx formulas.

| Aspect         | Canvas app detail                                                   |
| -------------- | ------------------------------------------------------------------- |
| Starting point | Blank screen, template, or data source                              |
| Layout control | Full control over every pixel and control placement                 |
| Data sources   | Any connector: Dataverse, SharePoint, SQL, Excel, and hundreds more |
| Logic          | Power Fx formulas, similar to Excel                                 |
| Best for       | Task-focused apps, mobile field apps, custom user experiences       |
| Runs on        | Web browser, and mobile through the Power Apps mobile app           |

Typical use cases:

| Use case                                   | Why canvas fits                                |
| ------------------------------------------ | ---------------------------------------------- |
| Site inspection app with photos on a phone | Custom layout, camera control, works on mobile |
| Event check-in app                         | Simple, single-purpose, fast to build          |
| Expense capture connected to SharePoint    | Mixes non-Dataverse data sources freely        |

## Model-driven apps

Model-driven apps are data-first. You model tables, forms, views, and business processes in Dataverse, and the app UI is generated with a consistent, responsive layout.

| Aspect         | Model-driven app detail                                 |
| -------------- | ------------------------------------------------------- |
| Starting point | Dataverse tables, forms, and views                      |
| Layout control | Limited; the platform generates a consistent UI         |
| Data sources   | Dataverse only (as the primary data platform)           |
| Logic          | Business rules, business process flows, Dataverse logic |
| Best for       | Complex, process-driven, data-heavy applications        |
| Navigation     | Sitemap with areas, groups, and pages                   |

Typical use cases:

| Use case                                 | Why model-driven fits                              |
| ---------------------------------------- | -------------------------------------------------- |
| Case management for a support team       | Many related tables, consistent forms and views    |
| Sales pipeline with stages and approvals | Business process flows guide users through stages  |
| Asset management across departments      | Data-heavy, role-based access, standard UI is fine |

### Canvas vs model-driven: the core comparison

| Question                | Canvas app                        | Model-driven app            |
| ----------------------- | --------------------------------- | --------------------------- |
| What drives the design? | The maker's layout (design-first) | The data model (data-first) |
| How much UI control?    | Total                             | Limited, generated          |
| Which data sources?     | Any connector                     | Dataverse                   |
| Typical size            | Focused task apps                 | Full business applications  |
| Skills needed           | Drag-and-drop plus Power Fx       | Data modeling in Dataverse  |

## Plan designer

Plan designer is an AI-first way to start a solution from a business problem instead of an app.

| Aspect      | Detail                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------- |
| Input       | A natural-language description of the business problem, optionally with files or images                  |
| Output      | A proposed plan: user roles, requirements, Dataverse tables, and suggested apps, agents, and automations |
| Value       | Turns one description into a coordinated multi-asset solution design                                     |
| Who uses it | Makers and teams starting a new solution                                                                 |

Exam cue: "describe the business problem and get a full solution blueprint (data plus apps plus agents)" is Plan designer, not just a canvas app Copilot prompt.

## Code apps

Code apps let professional developers build apps with traditional code (web technologies) and run them on Power Platform, so they get platform benefits without abandoning code.

| Aspect    | Detail                                                                |
| --------- | --------------------------------------------------------------------- |
| Who       | Professional developers                                               |
| What      | Apps written in code, hosted and run through Power Apps               |
| Why       | Reuse platform sign-in, connectors, governance, and management        |
| Fits when | Requirements exceed low-code tools but the org wants platform control |

Exam cue: "the development team wants to write real code but keep Power Platform governance and connectors" points to code apps.

## Building apps with AI

### Use AI to create a canvas app

| Step             | What happens                                                           |
| ---------------- | ---------------------------------------------------------------------- |
| Describe the app | Tell Copilot what the app should do in natural language                |
| Review the data  | Copilot proposes a Dataverse table (or uses your data / uploaded file) |
| Generate         | Copilot creates a working canvas app connected to that data            |
| Refine           | Ask Copilot for changes, or edit controls and Power Fx directly        |

### Use AI to create a model-driven app

| Step                   | What happens                                                              |
| ---------------------- | ------------------------------------------------------------------------- |
| Describe the solution  | Copilot proposes Dataverse tables, columns, and relationships             |
| Confirm the data model | Maker reviews and adjusts the proposed tables                             |
| Generate the app       | The model-driven app is generated from those tables, with forms and views |

### The vibe experience

The vibe experience is conversational, iterative app building: you chat with AI, it builds and updates the app, and you keep refining in natural language ("add a screen for managers," "make status a choice column," "show overdue items in red").

| Trait                  | Meaning                                                        |
| ---------------------- | -------------------------------------------------------------- |
| Conversational         | You build by chatting, not only by dragging controls           |
| Iterative              | Each prompt updates the working app                            |
| AI-powered apps        | Apps themselves can include AI capabilities for end users      |
| Maker still in control | You can inspect and manually edit everything that is generated |

Memory hook: Copilot generation gets you the first draft; the vibe experience is the ongoing conversation that shapes it.

## Common confusions

| Confusion                                   | Correct idea                                                                            |
| ------------------------------------------- | --------------------------------------------------------------------------------------- |
| Canvas vs model-driven                      | Canvas is design-first with any connector; model-driven is data-first on Dataverse      |
| Model-driven app vs Dataverse               | Dataverse stores the data model; the model-driven app is the generated UI on top        |
| Plan designer vs Copilot app generation     | Plan designer designs a whole multi-asset solution; Copilot generation drafts one app   |
| Code apps vs custom connectors              | Code apps are full coded applications; custom connectors wrap an API for low-code use   |
| Vibe experience vs Power Fx                 | Vibe is conversational AI building; Power Fx is the formula language you can still edit |
| Power Apps mobile vs separate mobile builds | One canvas app runs on web and mobile through the Power Apps mobile app                 |

## Exam traps

| Trap                                                          | Why people miss it                                                     |
| ------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Choosing model-driven for "full control of the screen layout" | Model-driven UI is generated; pixel control means canvas               |
| Choosing canvas for "app generated from our Dataverse model"  | That is the model-driven definition                                    |
| Thinking model-driven apps can use any connector as the base  | Model-driven apps are built on Dataverse                               |
| Treating Plan designer as only an app generator               | It proposes the broader plan: roles, tables, apps, agents, automations |
| Assuming AI-generated apps cannot be edited                   | Makers refine generated apps manually or with more prompts             |
| Assuming code apps bypass governance                          | The point of code apps is code plus platform governance                |

## Mini scenarios

| Scenario                                                                                      | Best answer                        |
| --------------------------------------------------------------------------------------------- | ---------------------------------- |
| Warehouse staff need a barcode-scanning app with a custom layout on phones.                   | Canvas app                         |
| A support team needs a case system over many related Dataverse tables with consistent forms.  | Model-driven app                   |
| A team lead describes an onboarding problem and wants AI to propose tables, apps, and agents. | Plan designer                      |
| Developers must build a complex coded UI but keep platform sign-in and connectors.            | Code apps                          |
| A maker types "build me an app to track laptop assignments" and gets a working draft app.     | Copilot / AI canvas app generation |
| The maker keeps chatting with AI to add screens and rules to the generated app.               | Vibe experience                    |
| The app needs Excel-like logic such as If(Price > 100, "High", "Low").                        | Power Fx                           |

## Check yourself

1. Which app type gives the maker full control over layout and works with any connector?
2. Which app type generates its UI from Dataverse tables, forms, and views?
3. What does Plan designer produce from a business problem description?
4. Who are code apps aimed at, and what do they gain from running on Power Platform?
5. Name the formula language used in canvas apps.
6. What is the vibe experience?
7. Can a model-driven app be built primarily on SharePoint lists?
8. After Copilot generates a canvas app, what are two ways the maker can change it?

## Answer guide

1. Canvas app.
2. Model-driven app.
3. A proposed solution plan: user roles, requirements, Dataverse tables, and suggested apps, agents, and automations.
4. Professional developers; they gain platform hosting, sign-in, connectors, governance, and management.
5. Power Fx.
6. Conversational, iterative AI app building: the maker chats with AI to create and refine an AI-powered app.
7. No. Model-driven apps are built on Dataverse.
8. Ask Copilot for changes in natural language, or edit the app directly (controls, screens, Power Fx).
