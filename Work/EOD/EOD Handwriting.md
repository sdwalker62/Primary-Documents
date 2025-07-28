> EOD has a requirement to extract text from forms containing hand writing. The form of the script can be in both cursive and print. Currently we have a form that has a QR code for aligning the form to the camera since the digital form capture is done manually and is not scanned in using a large-form scanner. 

# Prototyping Phase
`7/8/25 - 10/25/25`

- In the prototyping phase we will work with SERN resources and will have access to `4xA100` GPUs for training. Models will mostly be open although we should verify before the demo if it is an exotic or new model that might not be approved. Most ML frameworks are available (at least PyTorch and TensorFlow). Justin can provide a list of `pip` packages that are available. *The model **needs** to work with Nvidia Triton (23.10 currently)*.
	- Work on a Nvidia Triton Hello World for the team.
- In the prototyping phase we will gather representative hand-writing samples from different participants. We can print out the form made by Marchal and have people write different phrases and words that we have decided on beforehand. We should keep a mapping of participants to samples so we can gather accuracy metrics.
	- We should aim for around 30 participants so we can have a large enough sample.
	- The samples should contain both cursive and print formats.
	- Maybe give participants a timer to put pressure on them
	- Gather historical reports is not possible
	- Existing datasets might not contain representative phrases, acronyms, and words
	- Use left and right hand
	- Pencil vs Pen vs Marker
	- Different types of paper
	- Different color ink
	- Non-uniform lighting
- Experiment with the `gemma3` model as well as purpose-built models so we can compare different results. We should attempt to experiment with at least 3 models so we can examine their strengths and weaknesses.
	- Should consider models that are not multi-modal, but are built for OCR tasks.
- Some of the fields are not free text and are instead multichoice bubbles that the model will need to pick up.
- The deliverable should be a slide deck presenting results at a level the customer can understand and demonstrates the ROI. 
	- Part of the slide deck should include risks and COAs
		- Security concerns
		- Hardware concerns
		- etc.
- Determine an evaluation metric and a threshold and present it to the customer
	- The metric shouldn't be presented as a set of attributes ("Does consistently detecting matter to you")
		- Use these properties to figure out things like type-1 and type-2 error.
	- Determine buckets of thresholds that we need to meet (>95%, etc.)
- 