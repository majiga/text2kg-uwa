# Text2KG

UWA's submission to the ICDM2019 ICDM/ICBK Knowledge Graph Contest.

Team members:

- Wei Liu
- Majigsuren Enkhsaikhan
- Michael Stewart
- Morgan Lewis
- Thomas Smoker

## File structure
    
    datasets // Contains all contest-provided datasets
    sourcecode
        candidate_extraction    // Coref resolution + identifying noun and relation phrases
        triples_server          // Simple web server to communicate between visualisation app and triple models
        visualisation           // Visualisation web app
        requirements.txt        // All Python requirements for the /sourcecode directory
        setup.sh                // Creates a virtual environment and installs required packages
        run.sh                  // Runs the triple generation code
        

## Running the code

The sourcecode, available under the `/sourcecode` directory, may be run via the following commands:

    cd sourcecode
    chmod u+x setup.sh
    chmod u+x run.sh
    ./setup.sh
    ./run.sh

Please ensure you are using Python 3.6 and have the `virtualenv` package installed in order to maximise compatibility. Running the shell scripts will likely require a Unix-based OS such as Ubuntu.

## Visualisation web app

We have developed a Flask application that provides an easy-to-use interface for knowledge graph construction from text. Users may enter documents into a text box, click on the "Create graph" button, and their documents will be sent to our Candidate Extraction model for processing. An interactive graph will then be quickly be drawn to the screen.

If you wish to run the server locally, you must run the Visualisation server via:

    $ cd sourcecode/visualisation
    $ chmod u+x run_server.sh
    $ ./run_server.sh

The visualisation app will then be available at `localhost:5000` in a web browser.

You can also run `./run_server_gunicorn.sh` if you wish to run the server via wsgi.

## Running the visualisation with a different triple generation backend

It is possible to run the visualisation app with a different model for generating the triples. In line 39 of `sourcecode/visualisation/app/routes.py`, simply replace the `extract_triples` function with a different function that returns a list of triples, given a document. For example, if given the document `"Barrack Obama went to the Whitehouse with Michelle"`, the function must take that string as input and return a list of triples, e.g. `[["Barrack", "went to", "the Whitehouse"], ["Barrack Obama", "with", "Michelle"]... ]`.

## License

text2kg-uwa (c) by Michael Stewart, Majigsuren Enkhsaikhan and Wei Liu

text2kg-uwa is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.
