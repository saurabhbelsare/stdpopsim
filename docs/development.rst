.. _sec_development:

===========
Development
===========

``stdpopsim`` **is a community effort, and we welcome YOU to join us!**

We envision at least three main types of ``stdpopsim`` developers:

1. Demographic model contributors
2. API developers
3. Documentation and tutorial curators

`Demographic model contributors` add simulation code of published models.
This could be your own published model or any other published model you think
would be useful. This is the main way we envision biologists to continually add
to the catalog of available models, and it is a great first step for new
contributors to learn the ins and outs of ``stdpopsim`` development. See the
sections `Adding a new demographic model`_ and
`Demographic model review process`_ to get started.

`API developers` work on infrastructure development for the PopSim Consortium,
which could include improvements and additions to the internal code base of
``stdpopsim``, establishment of benchmarking pipelines,
and new projects that align with consortium goals.

`Documentation and tutorial curators` help maintain the documentation and tutorials.
This can be as easy as pointing out confusing bits of the documentation in a
GitHub `issue <http://github.com/popgensims/stdpopsim/issues>`_., or adding or editing
the documentation. See the section `Documentation`_.

Get into contact with the ``stdpopsim`` community by subscribing to our email list
`serve <https://lists.uoregon.edu/mailman/listinfo/popgen_benchmark>`_
and by creating and commenting on
Github `issue <http://github.com/popgensims/stdpopsim/issues>`_.
There is a lot of chatter through
`Github <http://github.com/popgensims/stdpopsim>`_, and we’ve been building code
there cooperatively.
If you want to help out and don't know where to start, you can look through the
list of
`Good first issues
<https://github.com/popgensims/stdpopsim/issues?q=is%3Aopen+is%3Aissue+label%3A%22
good+first+issue%22>`_
or
`Help wanted issues
<https://github.com/popgensims/stdpopsim/issues?q=is%3Aopen+is%3Aissue+label%3A%22
help+wanted%22>`_


To get started helping with ``stdpopsim`` development, please read the
following sections to learn how to contribute.
And, importantly, please have a look at our
`code of conduct <https://github.com/popsim-consortium/stdpopsim/blob/main/CODE_OF_CONDUCT.md>`_.

.. _sec_development_installation:

************
Installation
************

Before installing, be sure to make a fork of the repo and clone it locally
following the instructions in the `GitHub Workflow`_.

The ``stdpopsim`` library requires Python 3.4 or later.

For ``pip`` users, install the packages required for development using::

    $ python3 -m pip install -r requirements/development.txt

You can then install the development version of ``stdpopsim`` like this::

    $ python3 setup.py install

For ``conda`` users, you will need to add the conda-forge channel to your conda
environment and then should be able to install the development requirements using::

    $ conda config --add channels conda-forge
    $ conda install --file=requirements/development.txt


We do require ``msprime``, so please see the the `installation notes
<https://tskit.dev/msprime/docs/stable/installation.html>`_ if you
encounter problems with it.

.. Note:: If you have trouble installing any of the requirements, your ``pip`` may be the wrong version.
    Try ``pip3 install -r requirements/development.txt``

---------------------------
Using a Virtual Environment
---------------------------

We encourage the use of a virtual environment.

For ``pip``, you can use ``venv``.

First, create the virtual environment (You only need to do this once)::

    $ python3 -m venv stdpopsim_env

Next, activate the virtual environment::

    $ source stdpopsim_env/bin/activate

You will then see the virtual environment in your prompt. Like so::

    (stdpopsim_env) $

Once the virtual environment is activated, install the requirements::

    (stdpopsim_env) $ python3 -m pip install -r requirements/development.txt

You can then run any of the code in the virtual environment with the packages installed,
without conflicting with other packages in your local environment.
To deactivate the virtual environment::

    (stdpopsim_env) $ deactivate


***************
GitHub workflow
***************

    1. Make your own `fork <https://help.github.com/articles/fork-a-repo/>`_
       of the ``stdpopsim`` repository on GitHub, and
       `clone <https://help.github.com/articles/cloning-a-repository/>`_
       a local copy.
    2. Install the pre-commit hooks with::

        $ pre-commit install

    2. Make sure that your local repository has been configured with an
       `upstream remote <https://help.github.com/articles/configuring-a-remote-for-a-fork/>`_.
    3. Create a "topic branch" to work on. One reliable way to do it
       is to follow this recipe::

        $ git fetch upstream
        $ git checkout upstream/main
        $ git checkout -b topic_branch_name

    4. As you work on your topic branch you can add commits to it. Once you're
       ready to share this, you can then open a `pull request
       <https://help.github.com/articles/about-pull-requests/>`__. Your PR will
       be reviewed by some of the maintainers, who may ask you to make changes.
    5. If your topic branch has been around for a long time and has gotten
       out of date with the main repository, we might ask you to
       `rebase <https://help.github.com/articles/about-git-rebase/>`_. Please
       see the next section on how to rebase.

-----------------
Pre-commit checks
-----------------

On each commit a `pre-commit hook <https://pre-commit.com/>`_  will run
that checks for violations of code style and other common problems.
Where possible, these hooks will try to fix any problems that they find (including reformatting
your code to conform to the required style). In this case, the commit
will *not complete* and report that "files were modified by this hook".
To include the changes that the hooks made, ``git add`` any
files that were modified and run ``git commit`` (or, use ``git commit -a``
to commit all changed files.)

If you would like to run the checks without committing, use ``pre-commit run``
(but, note that this will *only* check changes that have been *staged*;
do ``pre-commit run --all`` to check unstaged changes as well).
To bypass the checks (to save or get feedback on work-in-progress) use
``git commit --no-verify``

--------
Rebasing
--------

Rebasing is used for two basic tasks we might ask for during review:

1. Your topic branch has gotten out of date with the tip of ``upstream/main``
   and needs to be updated.
2. Your topic branch has lots of messy commits, which need to be cleaned up
   by "squashing".

`Rebasing <https://help.github.com/articles/about-git-rebase/>`_ in git
basically means changing where your branch forked off the main code
in ``upstream/main``. A good way of visualising what's happening is to
look at the `Network <https://github.com/popgensims/stdpopsim/network>`_ view on
GitHub. This shows you all the forks and branches that GitHub knows about
and how they relate to the main repository. Rebasing lets you change where
your branch splits off.

To see this for your local repo
on your computer, you can look at the Git graph output via the command line::

    $  git log --decorate --oneline --graph

This will show something like:

.. code-block:: none

    |*   923ab2e Merge pull request #9 from mcveanlab/docs-initial
    |\
    | * 0190a92 (origin/docs-initial, docs-initial) First pass at development docs.
    | * 2a5fc09 Initial outline for docs.
    | * 1ccb970 Initial addition of docs infrastructure.
    |/
    *   c49601f Merge pull request #8 from mcveanlab/better-genomes
    |\
    | * fab9310 (origin/better-genomes, better-genomes) Added pongo tests.
    | * 62c9560 Tidied up example.
    | * 51e21e8 Added basic tests for population models.
    | * 6fff557 Split genetic_maps into own module.
    | * 90d6367 Added Genome concept.
    | * e2aaf95 Changed debug to info for logging on download.
    | * 2fbdfdc Added badges for CircleCI and CodeCov.
    |/
    *   c66b575 Merge pull request #5 from mcveanlab/tests-ci
    |\
    | * 3ae454f (origin/tests-ci, tests-ci) Initial circle CI config.
    | * c39415a Added basic tests for genetic map downloads.
    |/
    *   dd47000 Merge pull request #3 from mcveanlab/recomb-map-infrastructure
    |\

This shows a nice, linear git history: we can see four pull requests, each of
which consists of a small number of meaningful commits. This is the ideal that
we're aiming for, and git allows us to achieve it by *rewriting history* as
much as we want within our own forks (we never rewrite history in the
``upstream`` repository, as this would cause problems for other developers).
Having a clean, linear git history is a good idea for lots of reasons, not
least of which is making `git bisect <https://git-scm.com/docs/git-bisect>`_
easier.

One of the most useful things that we can do with rebasing is to "squash" commits
so that we remove some noise from the git history. For example, this PR
(on the branch ``topic_branch_name``) currently looks like:

.. code-block:: none

    $  git log --decorate --oneline --graph

    * 97a9458 (HEAD -> topic_branch_name) DONE!!!
    * c9c4a28 PLEASE work, CI!
    * ad4c807 Please work, CI!
    * 0fe6dc4 Please work, CI!
    * 520e6ac Add documentation for rebasing.
    *   20fb835 (upstream/main) Merge pull request #22 from mcveanlab/port-tennyson
    |\
    | * b3d45ea (origin/port-tennyson, port-tennyson) Quickly port Tennesen et al model.
    |/
    *   79d26b4 Merge pull request #20 from andrewkern/fly_model
    |\

Here, in my initial commit (520e6ac) I've added some updated documentation for rebasing.
Then, there's four more commits where I'm trying
to get CI pass. History doesn't need to know about this, so I can rewrite it
using rebase:

.. code-block:: none

    $ git fetch upstream
    $ git rebase -i upstream/main

We first make sure that we're rebasing against the most recent version of the
upstream repo. Then, we ask git to perform an interactive rebase against
the ``upstream/main`` branch. This starts up your editor, showing something
like this::

    pick 520e6ac Add documentation for rebasing.
    pick 0fe6dc4 Please work, CI!
    pick ad4c807 Please work, CI!
    pick c9c4a28 PLEASE work, CI!
    pick 97a9458 DONE!!!

    # Rebase 20fb835..97a9458 onto 20fb835 (5 commands)
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out

We want git to squash the last five commits, so we edit the rebase instructions
to look like:

.. code-block:: none

    pick 520e6ac Add documentation for rebasing.
    s 0fe6dc4 Please work, CI!
    s ad4c807 Please work, CI!
    s c9c4a28 PLEASE work, CI!
    s 97a9458 DONE!!!

    # Rebase 20fb835..97a9458 onto 20fb835 (5 commands)
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out

After performing these edits, we then save and close. Git will try to do
the rebasing, and if successful will open another editor screen that
lets you edit the text of the commit message:

.. code-block:: none

    # This is a combination of 5 commits.
    # This is the 1st commit message:

    Add documentation for rebasing.

    # This is the commit message #2:

    Please work, CI!

    # This is the commit message #3:

    Please work, CI!

    # This is the commit message #4:

    PLEASE work, CI!

    # This is the commit message #5:

    DONE!!!

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    #
    # Date:      Tue Mar 5 17:00:39 2019 +0000
    #
    # interactive rebase in progress; onto 20fb835
    # Last commands done (5 commands done):
    #    squash c9c4a28 PLEASE work, CI!
    #    squash 97a9458 DONE!!!
    # No commands remaining.
    # You are currently rebasing branch 'topic_branch_name' on '20fb835'.
    #
    # Changes to be committed:
    #       modified:   docs/development.rst
    #
    #

We don't care about the commit messages for the squashed commits, so we
delete them and end up with:

.. code-block:: none

    Add documentation for rebasing.

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    #
    # Date:      Tue Mar 5 17:00:39 2019 +0000
    #
    # interactive rebase in progress; onto 20fb835
    # Last commands done (5 commands done):
    #    squash c9c4a28 PLEASE work, CI!
    #    squash 97a9458 DONE!!!
    # No commands remaining.
    # You are currently rebasing branch 'topic_branch_name' on '20fb835'.
    #
    # Changes to be committed:
    #       modified:   docs/development.rst

After saving and closing this editor session, we then get something like:

.. code-block:: none

    [detached HEAD 6b8a2a5] Add documentation for rebasing.
    Date: Tue Mar 5 17:00:39 2019 +0000
    1 file changed, 2 insertions(+), 2 deletions(-)
    Successfully rebased and updated refs/heads/topic_branch_name.

Finally, after a successful rebase, you **must force-push**! If you try to
push without specifying ``-f``, you will get a very confusing and misleading
message:

.. code-block:: none

    $ git push origin topic_branch_name
    To github.com:jeromekelleher/stdpopsim.git
    ! [rejected]        topic_branch_name -> topic_branch_name (non-fast-forward)
    error: failed to push some refs to 'git@github.com:jeromekelleher/stdpopsim.git'
    hint: Updates were rejected because the tip of your current branch is behind
    hint: its remote counterpart. Integrate the remote changes (e.g.
    hint: 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.

**DO NOT LISTEN TO GIT IN THIS CASE!** Git is giving you **terrible advice**
which will mess up your branch. What we need to do is replace the state of
the branch ``topic_branch_name`` on your fork on GitHub (the ``upstream`` remote)
with the state of your local branch, ``topic_branch_name``. We do this
by "force-pushing":

.. code-block:: none

    $ git push -f origin topic_branch_name
    Counting objects: 4, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 4.33 KiB | 1.44 MiB/s, done.
    Total 4 (delta 2), reused 0 (delta 0)
    remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
    To github.com:jeromekelleher/stdpopsim.git
     + 6b8a2a5...d033ffa topic_branch_name -> topic_branch_name (forced update)

Success! We can check the history again to see if everything looks OK:

.. code-block:: none

    $  git log --decorate --oneline --graph

    * d033ffa (HEAD -> topic_branch_name, origin/topic_branch_name) Add documentation for rebasing.
    *   20fb835 (upstream/main) Merge pull request #22 from mcveanlab/port-tennyson
    |\
    | * b3d45ea (origin/port-tennyson, port-tennyson) Quickly port Tennesen et al model.
    |/
    *   79d26b4 Merge pull request #20 from andrewkern/fly_model
    |

This looks just right: we have one commit, pointing to the head of ``upstream/main``
and have successfully squashed and rebased.

------------------------
When rebasing goes wrong
------------------------

Sometimes rebasing goes wrong, and you end up in a frustrating loop of making
and undoing the same changes over and over again. First, here's an explanation
of what's going on. Let's say that the branch we're working on (and trying to
rebase) is called ``topic_branch``, and it branched off from ``upstream/main``
at some point in the past::

         A1---A2---A3  (topic_branch)
        /
    ---M---o---o---o---o---B  (upstream/main)

So, what we'd really like to do is to take the commits ``A1``, ``A2``, and
``A3`` and apply them to the current state of the ``upstream/main`` branch,
i.e., on top of commit ``B``. If we just do ``git rebase upstream/main``
then git will try to first apply ``A1``; then ``A2``; and finally ``A3``.
If there's conflicts, this is painful, so we might want to *first* squash
the three commits together into one commit, and then rebase that single commit.
Then we'll only have to resolve conflicts once. Said another way: we often
use ``git rebase -i upstream/main`` to both squash *and* rebase; but
it may be easier to squash first then rebase after.

We'll be doing irreversible changes, so first we should make a backup copy of
the branch::

    $ git checkout topic_branch  # make sure we're on the right branch
    $ git checkout -b topic_backup # make the backup
    $ git checkout topic_branch  # go back to the topic branch

Next, we take the diff between the current state of the files and the place
where your changes last diverged from ``upstream/main`` (the commit labelled
``M`` in the diagram above), and save it as a patch. To do this, make sure
you are in the root of the git directory, and::

    $ git diff --merge-base upstream/main > changes.patch

After that, we can check out a fresh branch and check if everything works
as it's supposed to::

    $ git checkout -b test_branch upstream/main
    $ patch -p1 < changes.patch
    $ git commit -a
    # check things work

After we've verified that everything works, we then checkout the original
topic branch and replace it with the state of the ``test_branch``, and
finally force-push to the remote topic branch on your fork::

    $ git checkout topic_branch
    $ git reset --hard test_branch
    $ git push -f origin topic_branch

Hard resetting and force pushing are not reversible operations, so please
beware! After you've done this, you can go make sure nothing bad happened
by checking that the only changes listed under "files changed" in the github
pull request are changes that you have made. For more on finding the fork
point, with diagrams, and an alternative workflow, see `the git docs
<https://git-scm.com/docs/git-merge-base>`__.

.. _sec_development_demographic_model:

******************************
Adding a new demographic model
******************************

Steps for adding a new demographic model:

1. `Fork the repository and create a branch`_
2. `Write the model function in the catalog source code`_
3. `Write parameter table`_
4. `Test the model locally`_
5. `Submit a Pull Request on GitHub`_

If this is your first time implementing a demographic model in `stdpopsim`, it's a good
idea to take some time browsing the :ref:`sec_catalog`
and species' demographic models in the
source code to see how existing models are typically written and documented. If you have
any questions or confusion about formatting or implementing demographic models, please
don't hesitate to open an `issue <http://github.com/popgensims/stdpopsim/issues>`_ --
we're more than happy to answer any questions and help get you up and running.

-----------------------------------
What models are appropriate to add?
-----------------------------------

`Stdpopsim` supports any demographic model from the published literature that gives
enough information to be able to define `msprime` demography objects. At a minimum, that
includes population sizes and the timing of demographic events. These values need to
either be given in "physical" units (that is, raw population sizes and time units in
generations), or be able to be converted to physical units using, e.g., mutation rates
used in the published study.

Note that it is not necessary that the demographic model is attached to a particular
species. `Stdpopsim` contains a collection of generic models that are widely used in
developing and testing inference methods. If there is a generic model that does not
currently exist in our catalog but would be useful to include, we also welcome those
contributions. Again, you should provide a citation for a generic models, or it
should be commonly used.

---------------------------------------
Fork the repository and create a branch
---------------------------------------

Before implementing any model, be sure to have forked the `stdpopsim` repository
and cloned it locally, following the instructions in the `GitHub Workflow`_ section.
Models are first implemented and tested locally, and then submitted as a pull request
to the `stdpopsim` repository, at which point it is verified by another developer
before being fully supported within `stdpopsim`.

---------------------------------------------------
Write the model function in the catalog source code
---------------------------------------------------

In the ``stdpopsim`` catalog source code (found in ``stdpopsim/catalog/``),
each species has a module that defines all of the necessary functions to run
simulations for that species, including the demographic model. In each species module,
you will see that each type of function is divided by comments, such as::

    ###########################################################
    #
    # Demographic models
    #
    ###########################################################

Go to the ``Demographic models`` section of the source code.
The demographic model function should follow this format:

.. code-block:: python

    def _model_func_name():
        id = "FILL ME"
        description = "FILL ME"
        long_description = """
        FILL ME
        """
        populations = [
            stdpopsim.Population(id="FILL ME", description="FILL ME"),
        ]
        citations = [
            stdpopsim.Citation(
                author="FILL ME",
                year="FILL ME",
                doi="FILL ME",
                reasons={stdpopsim.CiteReason.DEM_MODEL},
            )
        ]

        generation_time = "FILL ME"
        mutation_rate = "FILL ME"  # per bp per generation

        # parameter value definitions based on published values

        return stdpopsim.DemographicModel(
            id=id,
            description=description,
            long_description=long_description,
            populations=populations,
            citations=citations,
            generation_time=generation_time,
            mutation_rate=mutation_rate,
            population_configurations=["FILL ME"],
            migration_matrix=["FILL ME"],
            demographic_events=["FILL ME"],
        )


    _species.add_demographic_model(_model_func_name())


The demographic model should include the following:

* ``id``: A unique, short-hand identifier for this demographic model. This ``id``
  contains a short description written in camel case, followed by an underscore, and then
  four characters (the number of sampled populations, the first letter of the name of the
  first author, and the year the study was published). For example, the Gutenkunst et al.
  (2009) Out of Africa demographic model has the ``id`` "OutOfAfrica_3G09". See
  :ref:`sec_development_naming_conventions` for more details.
* ``description``: A brief one-line description of the demographic model.
* ``long_description``: A longer description (say, a concise paragraph) that describes
  the model in more detail.
* ``populations``: A list of ``stdpopsim.Population`` objects, which have their own
  ``id`` and ``description``. For example, the Thousand Genomes Project Yoruba panel
  could be defined as ``stdpopsim.Population(id="YRI", description="1000 Genomes YRI
  (Yorubans)")``.
* ``citations``: A list of ``stdpopsim.Citation`` objects for the appropriate citation
  for this model. The citation object requires author, year, and doi information, and
  a specified reason for citing this model.
* ``generation_time``: The generation time for the species in years. If you are
  implementing a generic model, the generation time should default to 1.
* ``mutation_rate``: The mutation rate assumed during the inference of this demographic
  model, per bp per generation, if a mutation rate was used. If no mutation
  rate is associated with this demographic model, which is generally uncommon
  but possible, depending on the inference method, the mutation rate should be
  set to ``None``.

Every demographic model has a few necessary features or attributes. First of all,
demographic models are defined by the population sizes, migration rates, split and
admixture times, and generation lengths given in the source publication. We often take
the point estimates for each of the values from the best fit model (for example, the
parameters that give the maximum likelihood fit), which are translated into
`msprime`-formatted demographic inputs.

`Msprime`-defined demographic models are specified through the
``population_configurations``, ``migration_matrix``, and ``demographic_events``. If this
is your first time specifying a model using `msprime`, it's worth taking some time to
read through the `msprime`
`documentation and tutorials <https://tskit.dev/msprime/docs/stable/quickstart.html>`_.


---------------------
Write parameter table
---------------------

The parameters used in the implementation must
also be listed in a csv file in the ``docs/parameter_tables`` directory. This ensures
that the documentation for this model displays the parameters.

Take a look at the csv files currently in ``docs/parameter_tables`` for inspiration.
The csv file should have the format::

    Parameter Type (units), Value, Description


We can check that the documentation builds properly after implementation by running
``make`` in the docs directory and opening the Catalog page from the ``docs/_build/``
directory. See `Documentation`_ for more details.


----------------------
Test the model locally
----------------------

Once you have written the demographic model function, you should test the model locally
with ``stdpopsim``. Follow the development :ref:`sec_development_installation`
instructions to install the development ``stdpopsim`` version along with the
requirements.

Now check that your new demographic model function has been imported:

.. code-block:: python

    import stdpopsim

    species = stdpopsim.get_species("HomSap")
    for x in species.demographic_models:
        print(x.id)

    # OutOfAfrica_3G09
    # OutOfAfrica_2T12
    # Africa_1T12
    # AmericanAdmixture_4B11
    # OutOfAfricaArchaicAdmixture_5R19
    # Zigzag_1S14
    # AncientEurasia_9K19
    # PapuansOutOfAfrica_10J19
    # AshkSub_7G19
    # OutOfAfrica_4J17


The example above lists the imported demographic models for humans.
You should substitute ``"HomSap"`` for which ever species you added your model to.
Your new model should be printed along with currently available demographic models.

.. note::

    If your demographic model does not print, after defining your model function,
    did you include the call ``_species.add_demographic_model(_model_func_name())``,
    where ``_model_func_name()`` is your model function name?

    If you are still having trouble, check the
    `GitHub issues <https://github.com/popsim-consortium/stdpopsim/issues?q=is%3Aissue+adding+demographic+model+>`_,
    or `open an issue <https://github.com/popsim-consortium/stdpopsim/issues/new>`_.

Next, check that you can successfully run a simulation with your new model with the
Python API. See :ref:`sec_python_tute` for more details.

-------------------------------
Submit a Pull Request on GitHub
-------------------------------

Once you have implemented the demographic model locally, including
documentation, the next step is to open a pull request with this addition.
See the `GitHub workflow`_ for more details.

---------------------------------------
So the model is implemented. What next?
---------------------------------------

Now at this point, most of your work is done!  The model is reviewed and
verified following the `Demographic model review process`_ by an independent member
of the development team, and there may be some discussion about formatting and
to clear up any confusing bits of the demographic parameters before the model is
fully incorporated into `stdpopsim`.

Thank you for your contribution, and welcome to the `stdpopsim` development team!

--------------------------------
Demographic model review process
--------------------------------

When Developer A creates a new demographic model on their local fork they must
follow these steps for it to be officially supported by stdpopsim:

    1. Developer A submits a PR to add a new model to the catalog. This includes
       full documentation (i.e., the documentation that will be
       rendered on rtd). The code is checked for any obvious problems/style
       issues etc by a maintainer and merged when it meets these basic
       standards. The new catalog model is considered 'preliminary'.

    2. Developer A creates an `issue
       <https://github.com/popsim-consortium/stdpopsim/issues/new/choose>`__
       tracking the QC for the model which includes information about the
       primary sources used to create the model and the population indices
       used for their msprime implementation. To create a new Model QC issue,
       click "New issue" from the "Issues" tab on GitHub, and click "Get
       started" to use the Model QC issue template. Follow the template to
       include the necessary information in the issue. Developer B is then
       assigned/volunteers to do a blind implementation of the model.

    3. Developer B creates a blind implementation of the model in the
       ``stdpopsim/qc/species_name.py`` file, remembering to register the
       QC model implementation (see other QC models for examples).  Note that
       if you are adding a new species you will have to add a new import to
       ``stdpopsim/qc/__init__.py``.

    4. Developer B runs the units tests to verify the equivalence of the
       catalog and QC model implementations.

    5. Developer B then creates a PR, and all being good, this PR is merged and
       the QC issue is closed.

------------------------
Arbitration
------------------------

When developers A and B disagree on the model implementation, the process is to:

    1. Try to hash out the details between them on the original issue thread

    2. If this fails, contact the authors of the original publication to resolve
       ambiguities.

    3. If changes have to be made to the production model Developer A submits a
       PR with the hotfix for the production model. Developer B then rebases
       the branch containing their PR against the main branch to check for model
       equality. Repeat steps 1-3 until this is achieved. If changes have to be
       made to the QC model they are committed to the branch where the QC PR
       originates from.

********************
Adding a new species
********************
To add a new species to `stdpopsim` several things are required:

1. The genome definition
2. Generation time estimate
3. Mutation rate (per generation)
4. Recombination rate (per generation)
5. Characteristic population size

A genetic map with local recombination rates is optional.

These parameters should be based on what values might be drawn from a typical population
as represented in the literature for that species. Consequently one or more citations for
each value are expected and will be required for constructing the species object detailed
below.

Once you have these things the first step is to create a new subdirectory of the `catalog/`
directory named for the species (see `Naming conventions`_ for more details). All
code described below should go in this directory unless explicitly specified otherwise.

-----------------------------------
Adding/Updating a genome definition
-----------------------------------

`stdpopsim` has an automated procedure for generating a genome definition, which is
accomplished by pulling data from Ensembl and saving it for parsing. To do this,
hand the `maintenance` command line interface a "_" delimited Ensembl species ID as a
positional argument as shown below. A partial list of the
genomes housed on Ensembl can be found `here <https://metazoa.ensembl.org/species.html>`__.

.. code-block:: shell

    python -m maintenance add-species arabidopsis_thaliana

This will generate new files inside `catalog/{species_id}/`:

* `genome_data.py`
* `species.py`
* `__init__.py`

as well as stubbing out tests in `tests/test_{species_id}.py`.

The `genome_data.py` file contains the physical map of the genome; the
`maintenance` utility sucks down a whole lot of useful information for free.
This file essentially puts together a data dictionary which has slots for the
assembly accession number, the assembly name, and a dict representing the
chromosome names and their associated lengths. If synonyms are defined (e.g.,
chr2L for 2L) then those are given in the list that follows. You double-check
the values, but probably there is no reason to edit this file.

Next, the `species.py` file will need to be edited with the species-specific
information and corresponding citations. Inside this file are commented
instructions for each section. Either chromosome-specific or genome-wide
recombination rates and mutations rates can be used at this stage; the
citations attached to these rates should be filled in inside the code block
beginning with `_genome`. For example, below is the _genome code block for
*A. thaliana* with citations included:

.. code-block:: python

    _genome = stdpopsim.Genome(
        chromosomes=_chromosomes,
        assembly_name=genome_data.data["assembly_name"],
        assembly_accession=genome_data.data["assembly_accession"],
        citations=[
            stdpopsim.Citation(
                author="Ossowski et al.",
                year=2010,
                doi="https://doi.org/10.1126/science.1180677",
                reasons={stdpopsim.CiteReason.MUT_RATE},
            ),
            stdpopsim.Citation(
                author="Huber et al.",
                year=2014,
                doi="https://doi.org/10.1093/molbev/msu247",
                reasons={stdpopsim.CiteReason.REC_RATE},
            ),
            stdpopsim.Citation(
                doi="https://doi.org/10.1093/nar/gkm965",
                year=2007,
                author="Swarbreck et al.",
                reasons={stdpopsim.CiteReason.ASSEMBLY},
            ),
        ],
    )


Generation time and population size, along with relevent citations, are filled
in inside the code block beginning with `_species`. It may be useful to look at
the existing species.py files inside the catalog/ directory for reference.

Once these fields have been entered, you should be able to load and simulate
the newly added species using `stdpopsim`.

However, the species still needs to be checked by someone else, i.e, QC'ed.
The maintenance script has also created a minimal set of tests in the file
`tests/test_{species_id}.py`. These tests should *not* be filled out by the
person who adds the species, but rather by someone else, as part of the
review process. However, some tests are already present,
and you can run them as follows:

.. code-block:: shell

   python -m pytest tests/test_AnoGam.py

This will check for things related to missing information and formatting. For
example, it checks that the citation year is of type `int` rather than `str`
(i.e., no quotes).

At some point during adding a species, you should start a pull request with your
changes. It does not have to be finished, since it's much easier for others to
help if they can see your code.

----------------------
Species review process
----------------------

Once everything works, we will merge your pull request, and the species will be
in stdpopsim, but still needs to go through a review process, in which someone else
checks parameters and citations as appropriate.  To initiate this process, open a
new `issue <https://github.com/popsim-consortium/stdpopsim/issues/new/choose>`__
using the 'Species QC issue template'. One or more volunteers will check items off
the checklist, until all items have been completed satisfactorily. The QC issue,
or the pull request, may be used for review discussion.

To begin reviewing (i.e., QC'ing) a species, you should state your intention on the
QC issue (so we don't duplicate effort) and start a pull request to fill out the code.
During the process of QC, other developers fill in the tests that are disabled
in the `tests/test_{species_name}.py` file by looking at the original papers
(not the implementation!) and filling in what they see to be the appropriate
values. For instance, a test for an unreviewed species might look like this:

.. code-block:: python

    @pytest.mark.skip("Recombination rate QC not done yet")
    @pytest.mark.parametrize(["name", "rate"], {}.items())
    def test_recombination_rate(self, name, rate):
        assert rate == pytest.approx(self.genome.get_chromosome(name).recombination_rate)

Looking at `tests/test_AedAeg.py`, we see this:

.. code-block:: python

    @pytest.mark.parametrize(
        ["name", "rate"],
        {"1": 0.306e-8, "2": 0.249e-8, "3": 0.291e-8, "MT": 0.0}.items(),
    )
    def test_recombination_rate(self, name, rate):
        assert rate == pytest.approx(self.genome.get_chromosome(name).recombination_rate)

The `@pytest.mark.skip` line has been deleted (because we should no longer skip
this test), and the dictionary (`{}`) in the `@pytest.mark.parameterize` line
has been filled out with key: value pairs that give the names and (mean) rates of
each chromosome. When we run tests (and, we can run only the *Aedes aegypti* tests
with `python -m pytest tests/test_AedAeg.py`), this will compare the values in the
tests file to the values loaded from stdpopsim (and error if they differ).
Filling out all these missing values in the tests file should get the species
entirely QC'ed. When it's done, we'll merge the PR and the species will be official!

Sometimes it's not clear which values to use (e.g., perhaps there are different
mutation rates estimated from two different groups of samples); in such cases
the original author should leave comments in the code explaining the choice,
and a note in the QC issue. If the values that the reviewer finds still do not
agree with the ones the original author found, they (and others) should discuss
on github about the best values to enter; once consensus is reached these can
be fixed up to agree in the QC pull request (i.e., you don't need to start
another pull request to change the values in the catalog itself).

********************
Adding a genetic map
********************

Some species have sub-chromosomal recombination maps available. They can be added to
`stdpopsim` by creating a new `GeneticMap` object and providing a formatted file
detailing recombination rates to a designated `stdpopsim` maintainer who then uploads
it to AWS. If there is one for your species that you wish to include, create a space
delimited file with four columns: Chromosome, Position(bp), Rate(cM/Mb), and Map(cM).
Each chromosome should be placed in a separate file and with the chromosome id in the
file name in such a way that it can be programatically parsed out. IMPORTANT: chromosome
ids must match those provided in the genome definition exactly! Below is an example start
to a recombination map file (see `here
<https://tskit.dev/msprime/docs/stable/api.html#msprime.RateMap.read_hapmap>`_
for more details)::

    Chromosome Position(bp) Rate(cM/Mb) Map(cM)
    chr1 32807 5.016134 0
    chr1 488426 4.579949 0

Once you have the recombination map files formatted, tar and gzip them into a single
compressed archive. The gzipped tarball must be FLAT (there are no directories in the
tarball). This file will be sent to one of the `stdpopsim` uploaders for placement in the
AWS cloud once the new genetic map(s) are approved. Finally, you must add a `GeneticMap`
object to the file named for your species in the `catalog` directory (the same one in
which the genome is defined) as shown below:

.. code-block:: python

    _genetic_map_citation = stdpopsim.Citation(
        doi="FILL_ME", author="FILL_ME", year=9999, reasons={stdpopsim.CiteReason.GEN_MAP}
    )
    """
    The file_pattern argument is a pattern that matches the recombination map filenames,
    where '{id}' is replaced with the 'id' field of a given chromosome.
    """
    _gm = stdpopsim.GeneticMap(
        species=_species,
        id="FILL_ME",  # ID for genetic map, see naming conventions
        description="FILL_ME",
        long_description="FILL_ME",
        url=("https://stdpopsim.s3-us-west-2.amazonaws.com/genetic_maps/dir/filename"),
        sha256="FILL_ME",
        file_pattern="name_{id}_more_name.txt",
        citations=[_genetic_map_citation],
    )

    _species.add_genetic_map(_gm)

The SHA256 checksum of the the genetic map tarball can be obtained using the
``sha256sum`` command from GNU coreutils. If this is not available on your
system, the following can instead be used:

.. code-block:: sh

   python -c 'from stdpopsim.utils import sha256; print(sha256("genetic_map.tgz"))'

Once all this is done, submit a PR containing the code changes and wait for directions
on whom to send the compressed archive of genetic maps to (currently Andrew Kern is the
primary uploader but please wait to send files to him until directed).

**************************
Lifting over a genetic map
**************************
Existing genetic maps will need to be lifted over to a new assembly, if and when the
current assembly is updated in `stdpopsim`. This process can be partially automated by running
the liftOver maintenance code.

First, you must download and install the ``liftOver`` executable from the
`UCSC Genome Browser Store <https://genome-store.ucsc.edu/>`_.
Next, you must download the appropriate chain files, again from UCSC
(see `UCSC Genome Browser downloads
<http://hgdownload.soe.ucsc.edu/downloads.html#liftover>`_ for more details).
To validate the remapping between assemblies it is required to have chain files
corresponding to both directions of the liftOver
(e.g. `hg19ToHg38.over.chain.gz` and `hg38ToHg19.over.chain.gz`) as in the
example below.

An example of the process for
lifting over the `GeneticMap` ``"HapMapII_GRCh37"`` to the ``"Hg19"`` assembly
is shown below:

.. code-block:: sh

    python /maintenance/liftOver_catalog.py \
        --species HomSap \
        --map HapMapII_GRCh37 \
        --chainFile hg19ToHg38.over.chain.gz \
        --validationChain hg38ToHg19.over.chain.gz \
        --winLen 1000 \
        --useAdjacentAvg \
        --retainIntermediates \
        --gapThresh 1000000

Here, the argument ``"--winLen"`` corresponds to the size of the window over which a weighted
average of recombination rates is taken when comparing the original map with the
back-lifted map (for validation purposes only). The argument ``"--gapThresh"`` is used to select a threshold for
which gaps in the new assembly longer than the ``"--gapThresh"`` will be set with a
recombination rate equal to 0.0000, instead of an average rate. The type of average rate used for gaps
shorter than the ``"--gapThresh"`` is determined either by using the mean rate of two most adjacent windows
or by using the mean rate for the entire chromosome, using options ``"--useAdjacentAvg"`` or
``"--useChromosomeAvg"``` respectively.

Validation plots will automatically be generated in the ``"/liftOver_validation/"``
directory. Intermediate files created by the ``liftOver`` executable will be saved
for inspection in the ``"/liftOver_intermediates/"``, only if the
``"--retainInermediates"`` option is used. Once the user has inspected the validation plots
and deemed the liftOver process to be sufficiently accurate, they can proceed to generating
the SHA256 checksum.

The SHA256 checksum of the new genetic map tarball can be obtained using the
``sha256sum`` command from GNU coreutils. If this is not available on your
system, the following can instead be used:

.. code-block:: sh

   python -c 'from stdpopsim.utils import sha256; print(sha256("genetic_map.tgz"))'

The newly lifted over maps will be formatted in a compressed archive and
automatically named using the assembly name from the chain file.
This file will be sent to one of the `stdpopsim` uploaders for placement in the
AWS cloud, once the new map is approved. Finally, you must add a `GeneticMap`
object to the file named for your species in the `catalog` directory (the same one in
which the genome is defined) as shown in `Adding a genetic map`_.

Again, once all this is done, submit a PR containing the code changes and wait for
directions on whom to send the compressed archive of genetic maps to
(currently Andrew Kern is the primary uploader but please wait to send files
to him until directed).

.. note::

    The ``GeneticMap`` named ``"ComeronCrossoverV2_dm6"`` for ``"DroMel"``
    was generated by similar code (albeit slightly different
    compared to that shown above) using the following command:

.. code-block:: sh

     python /maintenance/liftOver_comeron2012.py \
         --winLen 1000 \
         --gapThresh 1000000 \
         --useAdjacentAvg \
         --retainIntermediates


.. note::

    The ``GeneticMap`` named ``"SalomeAveraged_TAIR10"`` for ``"AraTha"``
    was generated by aligning the TAIR7 and TAIR10 with ``"minimap2"``,
    and lifting the recombination rates on TAIR7 to TAIR10 with
    ``"paftools.js liftover"``.


.. _sec_development_dfe_model:

******************
Adding a DFE model
******************

TODO: WRITE ME


****************
Coding standards
****************

To ensure that the code in ``stdpopsim`` is as readable as possible
and follows a reasonably uniform style, we require that all code follows
the `PEP8 <https://www.python.org/dev/peps/pep-0008/>`_ style guide.
Lines of code should be no more than 89 characters.
Conformance to this style is checked as part of the Continuous Integration
testing suite.

.. _sec_development_naming_conventions:

******************
Naming conventions
******************

To ensure uniformity in naming schemes across objects in ``stdpopsim``
we have strict conventions for species, genetic maps, and demographic
models.

Species names follow a ``${first_3_letters_genus}${first_3_letters_species}``
convention with capitilization such that Homo sapiens becomes "HomSap". This
is similar to the UCSC Genome Browser naming convention and should be familiar.

Genetic maps are named using a descriptive name and the assembly version according
to ``${CamelCaseDescriptiveName}_${Assembly}``. e.g., the HapMap phase 2 map on
the GRCh37 assembly becomes HapMapII_GRCh37.

Demographic models are named using a combination of a descriptive name,
information about the simulation, and information about the publication it was
presented in. Specifically we use
``${SomethingDescriptive}_${number_of_populations}${first_author_initial}${two_digit_date}``
where the descriptive text is meant to capture something about the model
(i.e. an admixture model, a population crash, etc.) and the number of populations
is the number of populations implemented in the model (not necessarily the number
from which samples are drawn). For author initial we will use a single letter, the 1st,
until an ID collision, in which case we will include the 2nd letter, and so forth.

DFEs (Distributions of Fitness Effects) are similarly named using something descriptive
of the distribution, and information about the publication:
``${SomethingDescriptive}_${First_authors_last_name_first_letter}{two_digit_date}``.
For instance, if the distribution in question is a lognormal distribution,
then ``LogNormal`` might be the descriptive string.


**********
Unit tests
**********

All code added to ``stdpopsim`` should have
`unit tests <https://en.wikipedia.org/wiki/Unit_testing>`_. These are typically
simple and fast checks to ensure that the code makes basic sense (the
entire unit test suite should not require more than a few seconds to run).
Test coverage is checked using `CodeCov <https://codecov.io/gh/popgensims/stdpopsim>`_,
which generates reports about each pull request.

It is not practical to test the statistical properties of simulation models
as part of unit tests.

The unit test suite is in the ``tests`` directory. Tests are run using the
`pytest <https://docs.pytest.org/en/stable/>`_ module. Use::

    $ python3 -m pytest

from the project root to run the full test suite. Pytest is very powerful and
has lots of options; please see the `tskit documentation
<https://tskit.dev/tskit/docs/stable/development.html#tests>`_ for help on
how to run pytest and some common options.

It's useful to run the ``flake8`` CI tests *locally* before pushing a commit.
To set this up use either ``pip`` or ``conda`` to install ``flake8``

To run the test simply use::

    $ flake8 --max-line-length 89 stdpopsim tests

If you would like to automatically run this test before a commit is permitted,
add the following line in the file ``stdpopsim/.git/hooks/pre-commit.sample``::

    exec flake8 --max-line-length 89 setup.py stdpopsim tests

before::

    # If there are whitespace errors, print the offending file names and fail.
    exec git diff-index --check --cached $against --

Finally, rename ``pre-commit.sample`` to simply ``pre-commit``

*************
Code Coverage
*************

As part of the continuous testing suite we have automated checking of how
well the test units cover the source code. As a result it's very helpful
to check locally how well your tests are covering your code by asking
`pytest` for coverage reports. This can be done with::

    $ pytest --cov-report html --cov=stdpopsim tests/

this will output a directory of html files for you to browse test coverage
for every file in `stdpopsim` in a reasonably straightfoward graphical
way. To see them, direct your web browser to the `htmlcov/index.html` file.
You'll be looking for lines of code that are highlighted yellow or red
indicated that tests do not currently cover that bit of code.


*************
Documentation
*************

Documentation is written using `reStructuredText <http://docutils.sourceforge.net/rst.html>`_
markup and the `sphinx <http://www.sphinx-doc.org/en/master/>`_ documentation system.
It is defined in the ``docs`` directory.

To build the documentation type ``make`` in the ``docs`` directory. This should build
HTML output in the ``_build/html/`` directory.

.. note::

    You will need ``stdpopsim`` to be installed for the build to work.


********************
Making a new release
********************

Here is a list of things to do when making a new release:

1. Update the changelog and commit
2. Create a release using the GitHub UI
3. `git fetch upstream` on your local branch.
    Then check out `upstream/main` and create a release tarball
    (with `python setup.py sdist`).
    Setuptools_scm will detect the version appopriately.
4. Upload to PyPI: `twine upload dist/{version just tagged}.tar.gz`
5. After the release, if everything looks OK,
   update the symlink for ``stable`` in the
   `stdpopsim-docs <https://github.com/popsim-consortium/stdpopsim-docs>`_
   repository
6. Check on the conda feedstock PR.
