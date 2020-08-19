# Lab Labels

A web service for making PDFs suitable for printing onto cryo-safe labels.
Built for biology labs.  Provides a web interface for human interaction and web
API for computer interaction.

## Installation

### À la carte

Lab Labels requires:

  - Perl 5.20 or newer
  - XeLaTeX
  - TeX Live
  - Droid package from TeX Live, if you don't have the full distribution

These can usually be installed via your operating system's package manager.

Once the above are installed, install the required Perl libraries by running:

    make deps

These will be installed into the `local/` directory, not your operating
system's default Perl library path.

Start the server with:

    ./local/bin/plackup

and open <http://localhost:5000> in your browser.

### Containerized with Docker

Build a `lab-labels` Docker image locally with:

    make docker-image

Then, start an ephemeral container with:

    docker run --rm --publish 5000:80 lab-labels

and open <http://localhost:5000> in your browser.

You can adjust the port mapping as you wish.  During development, a modified
version of the app can be overlaid into the container image like so:

    docker run --rm --publish 5000:80 --volume $PWD:/src lab-labels

The Docker image is not currently pushed to Docker Hub or any other image
repository, so you will have to build it yourself for now.

## Tips for printing

  - Use a laser printer or thermal roll printer.  Inkjet printing will rub off
    of most cryo-safe label paper.

  - Use a bypass paper tray if available.  Many laser printers, from low-end
    desktop printers to large multi-function printer/copier/fax machines,
    provide an alternate paper tray which keeps the paper flat instead of
    bending it around rollers.  You may need to install a printer driver
    specific to your make and model to have access to paper tray settings.

  - Set the paper type for the print job to "labels" and not "plain paper".
    Most printers will actually take into account the thicker label paper and
    produce better quality labels that are more legible.  Paper jams will also
    be less likely when the paper type is correctly set.  You may need to
    install a printer driver specific to your make and model to have access to
    paper type settings.

  - Disable page rescaling when printing.  The PDF pages are sized exactly to
    match the label sheets and rescaling can make the page smaller and misalign
    labels.

  - Orient the label paper correctly in the paper tray.  For example, the top
    left corner of the label sheets should match the location of the
    orientation symbols on the paper tray indicate.  Look on the paper itself
    for margin marks which indicate orientation.
