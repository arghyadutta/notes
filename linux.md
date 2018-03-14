* Example of setting proxy address in the .profile file

Use export for environment variables. Environment variables are an operating
system feature. Environment variables are inherited by child processes: if you
set them in a shell, they're available in all the programs started by this
shell. Variables used by many applications or by specific applications other
than shells are environment variables. For example in MPI

export http_proxy=http://www-proxy.mpip-mainz.mpg.de:8080
export https_proxy=http://www-proxy.mpip-mainz.mpg.de:8080
export no_proxy="127.0.0.1,localhost,.mpip-mainz.mpg.de"


