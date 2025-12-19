## Prompts for categorizing textual descriptions

These are the prompts we used to obtain the catergorization statistics in Fig. 8 using ChatGPT-o3. First, we need to upload the entire descriptions in the dataset to the ChatGPT-o3 web interface as a file and ask it to summarize a set of category labels that cover the entire dataset. Then, we ask ChatGPT to attribute each description sentence to this set of labels.   
The first step for obtaining the label set is prompted as follows. Depending on the quality of the output, it may require further checking and re-prompting.

```text
You are a video authenticity assessment expert. This is a video evaluation csv document where each line
contains an assessment statement of a video from a human annotator (the "descriptions_en" column).
You are now required to extract main catergorizations in three aspects: artifact location,
artifact type, and severity of artifact. These catergorizations may include the following:
Artifact locations (place): face, nose, eyes, eye-brows, mouth, teeth, contour, forehead, not-specified.
Artifact types (artifact): blur/out-of-focus, jitter/flickering, no apparent manipulation,
color/contrast anomaly, expression abnormality/stiffness, ghosting artifact, seam artifact,
distortion, asymmetry, lighting/shading anomaly, other.
Artifact Severity (extent): no-artifact, mild, moderate, sevear.
Please first analyze the entire file and evaluate whether the current categorization of location,
artifact type, and severity is comprehensive and sufficient to cover the entire cases in the file.
You may add new categories to either location or artifact type to improve coverage. Please
indicate which new categories you have added and explain their necessity.
```

Then we add the newly discovered categories to the set, and the second step for attributing each sentence is as follows.

```text
Attribute EACH sentence to these categories, and output ONE CSV file with the following columns: 
vid_names, descriptions_en, location, artifact, extent
vid_names: the source video filename of this sentence (keep as-is)
descriptions_en: the original sentence text (keep as-is)
place: one or more place labels, separated by semicolons ";"
artifact: one or more artifact labels, separated by semicolons ";"
extent: exactly one label from {no-artifact,mild,moderate,severe}
Use ONLY the label sets below (do not invent new labels).

============================================================
A) PLACE LABEL SET (14 facial regions)
============================================================
Choose one or more from:
- face
- not-specified
- mouth
- eyes
- teeth
- forehead
- nose
- chin
- contour
- cheeks
- eye-brows
- hairline
- neck
- ears

============================================================
B) ARTIFACT LABEL SET (19 artifact types)
============================================================
Choose one or more from:
- blur
- motion-blur
- flickering
- ghosting
- stiffness
- unnatural
- lighting-shadow
- color-contrast
- distortion
- asymmetry
- brightness
- mosaic
- frame-drop
- seam
- noise
- blocking
- artifact
- none
- others

============================================================
C) EXTENT LABEL SET (4-level severity)
============================================================
Choose exactly one from:
- no-artifact
- mild
- moderate
- severe

Some Rules:
1) mild:
   If the sentence contains mild modifiers such as:
   - a little, a bit, gentle, slight/slightly, subtle, mild

2) severe:
   Assign "severe" ONLY if at least one of the following holds:
   - Strong intensity words: obvious, severe, serious, strong, heavy, very, extreme, extremely

3) moderate (default):
   - If there is no explicit severity modifier (neither mild nor severe),
     default to "moderate".

============================================================
D) CSV OUTPUT REQUIREMENTS (STRICT)
============================================================
1) Output MUST be valid CSV text .
2) The first line MUST be the header:
   vid_names, descriptions_en, location, artifact, extent
3) One sentence per line (one CSV row).
4) If place or artifact has multiple labels, join them with semicolons ";" in a single cell.
```

Finally, we run a simple python script to sum the total appearance of each category over the entire dataset based on the above attribution output.

