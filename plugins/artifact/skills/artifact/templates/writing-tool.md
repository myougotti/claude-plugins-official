# Writing Tool Template

Use this template when the artifact helps shape writing: tone calibration, document structure planning, audience profiling, content briefs.

## Layout

```
+-------------------+----------------------+
|                   |                      |
|  Controls         |  Live text preview   |
|  grouped by:      |  (sample paragraph   |
|  • Tone           |   re-rendered with   |
|  • Audience       |   current settings,  |
|  • Structure      |   or outline skeleton)|
|  • Constraints    |                      |
|                   +----------------------+
|                   |  Prompt output       |
|                   |  [ Copy Prompt ]     |
+-------------------+----------------------+
```

## Control types by decision

| Decision | Control | Example |
|---|---|---|
| Tone axes | Slider pairs | formal↔casual, concise↔detailed, technical↔accessible |
| Audience expertise | Slider | beginner → expert |
| Audience role | Dropdown or chips | engineer, manager, exec, customer |
| Document sections | Drag-and-drop list | reorder outline items |
| Section depth | Per-item dropdown | brief / detailed / skip |
| Word/length constraints | Slider | target length 500–5000 words |

## Preview rendering

For tone tools, show a fixed sample paragraph and re-render it with exaggerated characteristics matching the sliders. This gives the user a feel for what "formal + concise" vs "casual + detailed" actually reads like.

```javascript
const SAMPLES = {
  formalConcise: "The system processes requests asynchronously via a distributed queue.",
  formalDetailed: "The system architecture relies on an asynchronous message queue to process incoming requests, ...",
  casualConcise: "It fires off requests in the background using a queue.",
  casualDetailed: "So basically, when a request comes in, it doesn't block — ...",
};

function renderPreview() {
  // Pick closest sample based on slider positions
  const key = closestSampleKey(state.formality, state.conciseness);
  document.getElementById('preview').textContent = SAMPLES[key];
}
```

For structure tools, render the outline as an indented list with section labels and depth tags.

## Prompt output for writing

Frame it as a writing direction with audience and style constraints:

> "Write a technical blog post about [TOPIC]. Target audience: mid-level engineers who know React but haven't used concurrent features. Tone: conversational but precise. Structure: intro (brief), problem statement (detailed), solution walkthrough with code examples (detailed), trade-offs (brief). Around 2000 words."

## Example topics

- Tone mixer (formal/casual × concise/detailed × technical/accessible — live sample)
- Document structure planner (outline builder with section types and depth)
- Audience profiler (expertise level, role, prior knowledge → writing prompt prefix)
- Content brief builder (topic + audience + structure + constraints → full writing prompt)
- Email drafting helper (recipient type, urgency, action needed → email prompt)
