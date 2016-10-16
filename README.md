# Useful Commands

This docker-image encapsulates the [dehydrated][dehydrated] cli tool which can be used to request [letsencrypt][letsencrypt] certificates. Just pull the image using:

    docker pull schoeffm/dehydrated

After importing the image just execute the followin':

    docker run --rm -ti schoeffm/dehydrated

Next, there is a more realistic command which uses a local `config`-file (which has to contains a `WELLKNOWN`-path that is under the control of your web-server). The resulting certificate is written to your local directory (which is also mounted as volume within the container).

    docker run --rm -ti \                                
        -v $(pwd):/cfg \                                 # mounts the current dir in the container
        --volumes-from <webContainer> \                  # also mount all dirs from the webserver
        schoeffm/dehydrated \ 
        -c -f /cfg/config -d <yourDomain> -o /cfg        # pass in all necessary arguments

[dehydrated]:https://github.com/lukas2511/dehydrated
[letsencrypt]:https://letsencrypt.org
