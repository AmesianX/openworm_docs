.. _muscle-neuron-integration:

******************
Muscle-Neuron Team
******************

.. contents:: Table of Contents

.. image:: http://docs.google.com/drawings/d/1WzHYpgHZBDvbAxIb-KDDw0OatI8KWXQ8h_BeMVaQ2wM/pub?w=1238&amp;h=869

.. _overview:

High-level Overview
===================

Broadly speaking, the team will develop a workflow and tools to simulate
*C. elegans* cell dynamics using simulated ion channel (*intracellular*)
dynamics.

Data mined from the relevant literature will be used to create ion channel
models. These ion channel models will be "embedded" in the virtual membranes
of simulated muscle cells and neurons, and give rise to electrophysical
dynamics for the cell as a whole.

All of these processes must have validation tests to ensure that each step is
doing exactly what we want it to do. This maintains the validity of the model as
 a whole, and provides breakpoints to examine if something in the workflow is
amiss.

It is especially important to validate the ion channel models we generate and
simulate, since it is at the deepest level of our model, and affects all other
layers on top of it.

This part of the workflow is described directly below.

.. _modelling-validation:

Modelling / Validation
======================

.. image:: https://docs.google.com/drawings/d/13JvpUktlTXN2GKH9fXzacXQWudm5MQUMXXY94cr6S50/pub?w=778&h=370

This figure shows, in a general way, how ion channel models are simulated and
incrementally fit to their observed counterparts.

Depending on the type of data being used (e.g. patch-clamp data or homology
modelling), the implementation will differ, but our approach will follow this
pattern.

Let's take an example channel model being compared to patch-clamp data from the
literature:

1. We have a given channel model (ex: `ca_boyle <https://github.com/openworm/muscle_model/blob/master/NeuroML2/ca_boyle.channel.nml />`_)
2. Run it through simulating scripts (ex: `Rayner's scripts <https://github.com/openworm/BlueBrainProjectShowcase/blob/master/Channelpedia/iv_analyse.py />`_)
3. These scripts give us a simulate I/V curve, which can be compared to a digitized I/V curve from the literature (`example digitized curve <https://plot.ly/~VahidGh/56/ />`_)
4. Depending on the result of `a test <https://github.com/openworm/muscle_model/issues/30 />`_ comparing these two I/V curves, the model is either *kept* or *optimized further* using NeuroTune.

.. _channelworm:

ChannelWorm
===========

`The ChannelWorm subproject <https://github.com/VahidGh/ChannelWorm/>`_ is, at a
high level, a pipeline to convert ion channel *data* found in scientific papers
into ion channel *models*. This pipeline involves:

1. `Identification <https://github.com/VahidGh/ChannelWorm/issues/10/>`_ of papers with ion channel data.
2. Extraction of data from these papers, including figures, active parameters and tabular data.
3. `Digitization <https://github.com/VahidGh/ChannelWorm/issues/17/>`_ of figures, and more generally, converting this information into machine-readable form.

..
  4. Fitting of models (to what? Is this part of the pipeline or validation process?)

..
  Previous accomplishments
  ------------------------



Current roadmap
---------------

We are tracking milestones for this project over `here. <https://github.com/VahidGh/ChannelWorm/milestones/>`_

The tasks ahead include:

1. Run `Rayner's scripts <https://github.com/openworm/BlueBrainProjectShowcase/blob/master/Channelpedia/iv_analyse.py/>`_ on an example cell, and get output.
2. Establish common format between outputs of Rayner's script (above) and `digitized plots <https://plot.ly/~VahidGh/56/>`_ from scientific articles.
3. Write test to compare digitized plots and plots generated from ion channel model.

Issues list
-----------

Issues for this part of the project are tracked and raised in `the Github repo. <https://github.com/VahidGh/ChannelWorm/issues?q=is%3Aopen+is%3Aissue/>`_

Associated Repositories
-----------------------

`ChannelWorm <https://github.com/VahidGh/ChannelWorm/ />`_

.. _neurotune:

Optimization (NeuroTune)
========================

The `Neurotune <https://github.com/vellamike/neurotune />`_  package provides neurotune a package for optimizing electical models of excitable cells.

Neurotune provides a solution for optimizing the parameters of a model to match
a specific output. In this case, the parameters are modelled ion channel
parameters, and the desired output is patch-clamp data comparable to that
observed in real life.

Associated Repositories
-----------------------

`Neurotune <https://github.com/vellamike/neurotune />`_
`NeuroTune docs <http://optimal-neuron.readthedocs.org/en/latest/architecture.html />`_

.. _pyopenworm:

PyOpenWorm
==========

`PyOpenWorm <https://github.com/openworm/PyOpenWorm/tree/master />`_ is a unified data access layer for OpenWorm. It's used to store and
retrieve data associated with *C. elegans*, associating evidence for this data
when it is stored.

Previous accomplishments
------------------------

* Create API to access data
* Create API to insert data
* Employ backend database to capture data

Current roadmap
---------------

PyOpenWorm will be used in the information storage aspect of various other
subprojects. For instance, ChannelWorm will use `its own fork of PyOpenWorm <https://github.com/openworm/PyOpenWorm/tree/channelworm />`_
to store Ion Channel data and models that it retrieves from scientific papers.
Next steps involve:

1. Adapting PyOpenWorm's existing infrastructure to serve ChannelWorm
2. Filling the database with information, being sure to tag each fact with sources along the way.

Issues list
-----------

Issues for PyOpenWorm are tracked `on Github <https://github.com/openworm/PyOpenWorm/issues />`_.

Associated Repositories
-----------------------

`PyOpenWorm <https://github.com/openworm/PyOpenWorm/ />`_

.. _musclemodel:

Muscle Model
============

The `muscle model subproject <https://github.com/openworm/muscle_model />`_ is concerned with modelling and simulation at the
*cellular* level, specifically attempting to simulate the electrical dynamics of
 a *C. elegans* body wall muscle cell.

This depends on what happens in the :ref:`channelworm` repo, since ion channel
dynamics are integral to our simulation of membrane dynamics.

Previous accomplishments
------------------------

* Implementation of Boyle & Cohen muscle model `in python <https://github.com/openworm/muscle_model/tree/master/BoyleCohen2008 />`_
* `Conversion of model into NEURON <https://github.com/openworm/muscle_model/tree/master/neuron_implementation />`_
* `Simulation <https://github.com/openworm/muscle_model#21-simulation-of-muscle-cell-ion-channels />`_ of NeuroML2 ion channels in LEMS

Current roadmap
---------------

Some of the next steps for the muscle model subproject include:

1. Write validation tests for the muscle model (Ex: using `SciUnit <https://github.com/scidash/sciunit />`_).
2. Run validation tests.

Issues list
-----------

Issues for the muscle model are tracked `on Github. <https://github.com/openworm/muscle_model/issues />`_

Associated Repositories
-----------------------

`Muscle_model <https://github.com/openworm/muscle_model />`_

.. _c302:

c302
====

The `c302 subproject <https://github.com/openworm/CElegansNeuroML/tree/master/CElegans/pythonScripts/c302 />`_
is an effort to simulate the connectome of *C. elegans*, which includes its 302
 neurons. The neural dynamics will start out with biologically-unrealistic
 integrate and fire cells, and be replaced with incrementally more realistic
 dynamics, as tests pass. Like the :ref:`musclemodel`, dynamics of neurons
 depend on ion channel dynamics within the cells, and thus depend on the
 :ref:`channelworm` subproject.

Previous accomplishments
------------------------

* Generate NeuroML2 using `libNeuroML <https://github.com/NeuralEnsemble/libNeuroML />`_ combined with connectivity data
* Run simulations of the connectome in LEMS using `jNeuroML <https://github.com/NeuroML/jNeuroML />`_ or `pyNeuroML <https://github.com/NeuroML/pyNeuroML />`_

Current roadmap
---------------

1. Create validation tests using `SciUnit <https://github.com/scidash/sciunit />`_ or a similar framework.
2. Run validation tests.

Issues list
-----------

Issues for :ref:`c302` are tracked `in the CElegansNeuroML repo. <https://github.com/openworm/CElegansNeuroML/issues />`_

Associated Repositories
-----------------------

`CElegansNeuroML <https://github.com/openworm/CElegansNeuroML />`_
