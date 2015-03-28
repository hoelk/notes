Geopython
#########

Setup virtal environemtn
========================

.. code-block:: bash

    sudo pip install virtualenv
    virtualenv my_environment_name
    ./activate

    pip list # to list installed packages


List comprehension
==================

.. code-block:: python

    dataset1= [1,2,3,4]

    print(dataset1)
    result = [k**2 for k in dataset1] # {} for dict comprehension
    print(result)


CLI
===

.. code-block:: python

    # Simple CLI
    if __name__ == '__main__':
        import sys
        print sys.argv

    # Advanced CLI
    import argparse
    if __name__ == '__main__':
        parser = argparse.ArgumentParser(
            description="get the given name, optionally also the surname")
        parser.add_argument("given_name", help="given name of the person")
        parser.add_argument(
            "‐s", "‐‐surname", help="the surname of the person")
        args = parser.parse_args()
        print(args.given_name)
        if args.surname:
            print(args.surname)


Try-Except Block
================

.. code-block:: python

    def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print "division by zero!"
    else:
        print "result is", result
    finally:
        print "executing finally clause"
        
    divide(2, 1)
    divide(2, 0)
