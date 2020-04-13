# ros-singularity
Setup for ROS in a Singularity Container

## Installation

Follow the official [Singulariy Documentation](https://sylabs.io/guides/3.5/user-guide/) for the Singularity Setup.

Go into the images folder and run:

```bash
sudo singularity build <name>.simg Singularity.<distro>
```

## Personal Recommendation

My images all follow the pattern: ros-\<distro\> and are moved to a folder in my home directory.  
This makes it possible to use the following bash functions a quick start of the container from anywhere and autocompletion of this command.

**Quickstart a Container from anywhere:**
```bash
ros() {
  singularity shell ~/<singularity-image-folder>/ros-$1.simg -c "source /opt/ros/$1/setup.bash"
}
```

**Enable Autocompletion for the image names:**
```bash
_ros() {
  local cur=${COMP_WORDS[COMP_CWORD]}
  COMPREPLY=( $(compgen -W "$(ls ~/<singularity-image-folder> | sed 's/.\{5\}$//' | sed 's/.\{4\}//')"))
}
complete -F _ros ros
```
[More Information about the Autocompletion](http://fahdshariff.blogspot.com/2011/04/writing-your-own-bash-completion.html)


## Contributing
Pull Requests with new Singularity Images for older or newer versions of ROS are welcome.

## License
[MIT](https://choosealicense.com/licenses/mit/)