### Playblasting in Maya done with GUI

A visual interface for
[maya-capture](https://github.com/abstractfactory/maya-capture).

<img align="right" src="https://cloud.githubusercontent.com/assets/2439881/18627536/c1a6b4e4-7e5b-11e6-9c69-047bd5cbbce5.jpg"/>

> WARNING: Preview release

<br>

### Features

- Set up your playblasts visually (with direct feedback). 
- Produce consistent predictable playblasts.
- Callbacks to allow custom encoding prior to opening viewer.
- Avoid unwanted overscan; playblast what you render.

<br>

### Installation

To install, download this package and [capture](https://github.com/abstractfactory/maya-capture)
and place both in a directory where Maya can find them.

<br>

### Usage

To show the interface in Maya run:

```python
import capture_gui
capture_gui.main()
```

<br>

### Advanced

Register a pre-view callback to allow a custom conversion or overlays on the 
resulting footage in your pipeline (e.g. through FFMPEG)

```python
import capture_gui

# Use Qt.py to be both compatible with PySide and PySide2 (Maya 2017+)
from capture_gui.vendor.Qt import QtCore

def callback(options):
    """Implement your callback here"""

    print("Callback before launching viewer..")

    # Debug print all options for example purposes
    import pprint
    pprint.pprint(options)

    filename = options['filename']
    print("Finished callback for video {0}".format(filename))


app = capture_gui.main(show=False)

# Use QtCore.Qt.DirectConnection to ensure the viewer waits to launch until
# your callback has finished. This is especially important when using your
# callback to perform an extra encoding pass over the resulting file.
app.viewer_start.connect(callback, QtCore.Qt.DirectConnection)

# Show the app manually
app.show()
```


### Known issues

The Viewport Plugin has a menu which displays all the shapes who's visibility can
be toggled in the viewport. Depending on the position of the menu, when creating a tear off version
of the menu, it might be unable to close it because the title bar is not visible.
Ensure the focus in on the menu and press Alt+F4 or use Alt+Space to show the window control menu
through which you can close the window.