# Documentation & Visual Assets

This directory contains the graphical assets and icons used to support the data storytelling and animations within the project.

### 🖼️ Animation Assets (Manim)
These files are utilized as `ImageMobject` elements within the `02_story.ipynb` notebook to enhance the visual narrative of the horse population evolution.

*   **horse_icon.png**: A visual anchor used in the introduction.
*   **manim_logo.png**: Used in the final scene to acknowledge the animation engine used for the project rendering.

### ⚙️ Usage in Code
In the Manim animation script, these assets are accessed via predefined paths:

```python
HORSE_ICON_PATH = "../docs/icons/horse_icon.png"
MANIM_ICON_PATH = "../docs/icons/manim_logo.png"