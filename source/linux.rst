Linux
#####

Tricks
======

.. code-block:: bash

  locate firefox.desktop # find desktop files


Replace in all files in directory

.. code-block:: bash

    find ./ -name \*.R -exec sed -i "s/allance/alance/g" {} \;


Setup git
=========

1. Inital setup

  .. code-block:: bash

    git config --global user.name "YOUR NAME"
    git config --global user.email "YOUR EMAIL ADDRESS"

    cd ~/your/project
    git init
    git remote add origin https://github.com/yourusername/Hello-World.git

2. Your first commit

  .. code-block:: bash

    git add . # add all files in the directory
    git commit -m 'first commit' # commit (locally)
    git push origin master # upload to github

3. Save credentials so you dont have to enter them every time you push

  .. code-block:: bash

    git config --global credential.helper cache




Samba
=====

.. code-block:: bash

  net usershare add Sharename /pfad/zu/ordner "Kommentar" Everyone:f guest_ok=y  # Everyone:r to allow only read access
  sudo service smbd restart
