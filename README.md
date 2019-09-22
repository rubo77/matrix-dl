# matrix-dl


Download backlogs from Matrix as raw text

Fork of https://gitlab.gnome.org/yarikoptic/matrix-dl

JFYI, @thiblahute was developed a simple but useful command line for this:
https://gitlab.gnome.org/thiblahute/matrix-dl

# install 

### create a virtual environment

In order to install `matrix-dl` without messing our system's Python setup, we will document how to install it using a virtual environment. The command `virtualenv` is provided by a Python package that enables the creation of these virtual environments. You can install `virtualenv` using you packaging system, for example on Debian:

    sudo apt install virtualenv

Or with pip:

- Install pip first: `sudo apt-get install python3-pip`
- Then install virtualenv using `pip3 install virtualenv`

### Then run:

    mkdir -p ~/matrix-dl-env
    cd ~
    virtualenv -p python3 matrix-dl-env
    cd matrix-dl-env
    source bin/activate

    # Clone the code
    git clone https://github.com/rubo77/matrix-dl
    cd matrix-dl

    # install dependencies and the script itself in the virtual environment:
    python setup.py install

# Usage:

The tool's usage instructions are these:

    matrix-dl [-h] [--password PASSWORD] [--matrix-url MATRIX_URL]
             [--start-date START_DATE] [--end-date END_DATE]
             username room

The `MATRIX_URL` is the bit at the end of your username. So if my account was `@someone:matrix.org` then `https://matrix.org` would be the `MATRIX_URL`.

## Download backlogs from Matrix as raw text

    positional arguments:
     username                Your username without @ and without the MATRIX_URL part
     room                    Room-ID without the MATRIX_URL part or Alias of the room

    optional arguments:
     -h, --help               show this help message and exit
     --password PASSWORD      Will be asked later if not provided
     --matrix-url MATRIX_URL  without trailing slash
     --start-date START_DATE  format %d%m%Y
     --end-date END_DATE      format %d%m%Y

### A couple examples:

Let's download the conversations from Example channel since the beginning of 2018:

    matrix-dl --matrix-url https://matrix.example.com --start-date 01012018 \
     <fsurname> "Example" > example-2018.log

Then you will be asked for you password, and if there is no errors, the conversations will be dumped in the file `example-2018.log` with the format `hh:mm:ss — @user: message`

You can also dump conversation from unnamed rooms, such as personal conversation, you just need the room's internal ID. You can get this string in riot by clicking in the room's settings icon (the gear so far) and at the end of the settings, in the advanced section, there's the room's ID:

    matrix-dl --matrix-url https://matrix.example.com --start-date 01012018 \
     <fsurname> \!i4BiDaYPkvfbcWdAgb:example.com > my-chat-2018.log

Remember to escape the symbol !, otherwise the shell will consider it an operator.
