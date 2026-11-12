# Introduction
This is a simple benchmark for express evaluation of LLMs. Download the shg_bench. Give the AI agent the task: "Complete the task **[path]**\shg_bench\task.txt". Evaluate the result following the evaluation methodology, or simply compare it visually with the results of other models.
**[path]** — the local directory where the benchmark is placed.

# How it works
The agent is given a single prompt to create a photorealistic and atmospheric 3D scene of Stonehenge, including 3D models, texture mapping, particle effects, and lighting. The result must be an HTML file that can run standalone in an isolated environment (with no links to assets or other resource files). A common evaluation methodology is included with the benchmark so that a leaderboard can be compiled. However, the benchmark's primary purpose is to quickly verify that a model works correctly after local deployment, to compare different quantizations and inference settings, or to check the quality of models that do not yet have results on major authoritative benchmarks. 
**Average test duration:** 15–120 minutes. 
**Result:** an HTML file that runs the scene. Contents: a prompt describing the task and the rules, plus a set of assets with textures that the agent is allowed to use while solving the task.
**Subject of evaluation:** the harness in combination with the LLM. 
It is recommended to use a clean harness without additional skills or external tools.

# Promt
_"Create a photorealistic, real-time Three.js scene of Stonehenge as it stands today in Wiltshire._

_It’s night. Strong wind drives light rain across the plain. A bright moon and occasional lightning near the horizon are the only light on the stones. Soft cloud shadows drift across the grass and stone. At the center, a few people warm themselves around a campfire. Make that small circle of warmth feel sheltered amid the storm._

_Show the scene in a continuous, medium-wide automatic orbit from above, with the camera aimed 30° below horizontal. Hold the right mouse button and drag horizontally to orbit or vertically to tilt. Scroll the mouse wheel to zoom in or out._

_Rules_
_- Work from this prompt alone. No follow-up questions, subagents, or additional AI models, including image and 3D generators._
_- Build the geometry yourself. Use only visuals you create during this run or find in ./assets/. No stock assets, ready-made scenes, or previous solutions._
_- No web search or browsing. Network access is allowed only to install libraries and tools. You may render, inspect, and refine your work locally._
_- Submit exactly one self-contained .html file. Embed Three.js and every script, stylesheet, and asset the scene uses"_ **\***
**\* - this prompt is stored in the benchmark resourses and is not passed to the agent harness in the chat. The launch process is described in the introduction**

# Evaluation methodology
To determine the LLM score using the unified methodology and to compile a leaderboard table, simply rate the scene against each of the 10 criteria described below. A model can score from 0 to 2 points on each criterion. Then add up all the points, divide the result by 20, and multiply by 100. In this way, the model will receive a score from 0 to 100 points (in 5-point increments). 
If, as a result of the run, no HTML file is produced or the scene does not start, the model's overall score is 0 points.

| № | Evaluation subject | Question | 0 points | 1 point | 2 points |
|---|---|---|---|---|---|
| 1 | Architecture recognizability | How faithfully is the Stonehenge architecture reproduced? | Just a pile of stones arranged in a circle | A few recognizable elements are present | The architecture is reproduced accurately; all key elements are present |
| 2 | Stone models | How well are the 3D models of the stones made? How well are they textured? How photorealistic are they? | Low-polygon models, unrealistic or missing textures, many artifacts and errors | The models are not very realistic, but on the whole they look tidy, the textures are in place, and there are no obvious artifacts | Realistic high-polygon stone models, high-quality textures; the stones look realistic |
| 3 | People models | How well are the 3D models of the people made? Are there textures and animation? How realistic do they look? | The models are low-polygon, animation is absent or minimal, there are no textures, or there are serious errors and artifacts in the models | The models are not perfect, but they look tidy and atmospheric. The light from the campfire falls on them, there is basic animation, and there are no serious model defects | Excellent, lively-looking animated models. Textures are present. Nice little touches and details are implemented that add atmosphere to the scene |
| 4 | Lighting | How well is the lighting done? The overall contrast of the scene, the shadows matching the light sources, highlights, reflections? | The scene is too dark or, conversely, as bright as day; shadows are missing or fall in the wrong direction; poor, unrealistic lighting | The light sources of the moon and the campfire are configured correctly. Shadows are present and fall in the right direction. But the quality of the shadows and reflections is imperfect | The lighting is flawless: there are drifting cloud shadows; the soft shadows of the stones repeat their shape exactly. There are wet-stone effects and puddles on the rain-soaked ground in which the light is reflected; the lighting from the campfire and from the drifting clouds in the sky is dynamic and alive |
| 5 | Particle effects | How realistically are the particle effects implemented in the scene: the rain and the campfire? | One or both effects are missing, contain obvious errors and artifacts, or look completely unrealistic. For example: no animation — the fire or the rain is static, the rain has no volume, the campfire is made of simple primitives, etc. | Most of the required particles are present and look decent: there is fire, sparks and smoke; the rain has depth and falls from top to bottom throughout the scene's space | All the effects are present and look excellent. Additionally, gusts of wind are felt that affect the fire, the smoke and the rain; or the raindrops are rendered, or there is fog or other small touches that add realism to the scene |
| 6 | Ground surface and horizon | How well is the plain on which Stonehenge stands made? | A flat surface, without volume, texture or details. Or with minimal details | The surface has volume and texture. A basic implementation of grass and unevenness. The horizon line is well thought out, with trees or other objects visible along it | A highly detailed, carefully designed plain. It is not flat but has good, deliberate relief. The texture is high-quality, varied and realistic. The grass sways in the wind; the horizon is also implemented well |
| 7 | Sky | How well and realistically is the sky done? | A completely black or gray sky without details, or with a basic static texture. The moon is missing or implemented at a basic level. Or there are serious artifacts in the texture placement | The sky has a good texture without stitching artifacts and a basic animation. The moon is in place and looks decent; no serious issues | The sky texture has depth and lighting work, as well as an animation of drifting clouds. Lightning flashes are also reflected on the clouds. The moon also has a texture and can be covered by the drifting clouds |
| 8 | Lightning | How well are the lightning discharges implemented? | Lightning discharges are missing or implemented at a basic level. The lightning is drawn as a simple line that appears and disappears entirely, without effects or volume. There is no reflection from the flash | The lightning has a realistic shape. The discharge is clearly felt thanks to its reflection on the stones and the ground | The lightning is implemented flawlessly. It is drawn realistically. The discharge begins in the sky and only then strikes the ground. The discharge effectively lights up the clouds as well, not only the ground and the stones; the raindrops are also illuminated, the people react to the discharge, or there are additional details that add atmosphere to the lightning |
| 9 | Artifacts | Rate the total number of artifacts and defects in the scene. Defects mean obvious errors in models, textures, effects or animations: extra arms on people, static objects that should be moving, overlapping and incorrect texture seams, objects hanging in the air, etc. | 4 or more defects recorded | No more than two defects recorded | No obvious defects recorded |
| 10 | Atmosphere | Give an overall assessment of the scene's composition as a whole. How do all the objects and details feel together? How well do the colors and objects combine? How atmospheric and realistic did the scene turn out? | The scene does not read at all: it is too dark or too bright, or critical defects make it impossible to judge. There is no realism whatsoever either — the crudest primitives, no textures and a multitude of artifacts | The scene is generally tidy and atmospheric. There is room for improvement, but it is not bad | All the details look harmonious and are executed at a high level. The composition and the sense of immersion are excellent |


# Leaderboard

| Model | Quant | Harness | Context | Reasoning effort | Provider | Result path | Final score | Architecture recognizability | Stone models | People models | Lighting | Particle effects | Ground surface and horizon | Sky | Lightning | Artifacts | Atmosphere |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| GPT6 Astra | ? | Codex | ? | Extra high | OpenAI | GPT6Astra_Codex_1.html | 70 | 1 | 2 | 1 | 1 | 2 | 2 | 1 | 2 | 1 | 1 |
| Qwen4 Max Preview | ? | Qoder | ? | N/A | Alibaba | Qwen4MaxPreview_Qoder.html | 40 | 0 | 0 | 0 | 2 | 1 | 1 | 1 | 1 | 1 | 1 |
| GPT5.6 Sol | ? | Codex | ? | Extra high | OpenAI | GPT5.6Sol_Codex_1.html | 35 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 1 |
| GLM5.3 | ? | Qoder | ? | N/A | Alibaba | GLM53_Qoder_1.html | 25 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 2 | 0 | 1 |
| Qwen3.8 flash next | NVFP4 | Hermes agent | 262k | N/A | Local | Qwen38FN_Hermes_nvfp4_1.html | 20 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 1 |
| GPT5.6 Luna | ? | Codex | ? | Extra high | OpenAI | GPT56Luna_Codex_1.html | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |


You can send me your resulting HTML files, along with the exact model and harness used, and I will include them in the leaderboard. Please use a clean harness, without additional skills and tools, so that the evaluation is accurate.
