.. . Kicking page rebuild 2014-10-30 17:00:08

.. index:: Bid, Parameter, LotValue, bidder, participant, pretendent

.. _bid:

Bid
===

Schema
------

:tenderers:
    List of :ref:`Organization` objects

:date:
    string, :ref:`date`, autogenerated

:id:
    uid, autogenerated

:status:
    string

    Possible values are:

    * `draft`
    * `pending`
    * `active`
    * `invalid`
    * `invalid.pre-qualification`
    * `deleted`

:value:
    :ref:`Value`, required

    Validation rules:

    * `amount` should be less than `Tender.value.amout`
    * `currency` should either be absent or match `Tender.value.currency`
    * `valueAddedTaxIncluded` should either be absent or match `Tender.value.valueAddedTaxIncluded`

:parameters:
    List of :ref:`Parameter` objects

:lotValues:
    List of :ref:`LotValue` objects

:participationUrl:
    url

    A web address for participation in auction.

There are several `envelopes` - document containers that manage time when their information will be revealed:

:documents:
    This envelope has to contain (`technicalSpecifications` and `qualificationDocuments`). It is revealed at pre-qualification.

:financialDocuments:
     This envelope can contain financial part of proposal (`commercialProposal`). It is revealed at post-qualification.
    
.. _Parameter:

Parameter
=========

Schema
------

:code:
    string, required

    Code of the feature.

:value:
    float, required

    Value of the feature.

.. _LotValue:

LotValue
========

Schema
------

:value:
    :ref:`Value`, required

    Validation rules:

    * `amount` should be less than `Lot.value.amout`
    * `currency` should either be absent or match `Lot.value.currency`
    * `valueAddedTaxIncluded` should either be absent or match `Lot.value.valueAddedTaxIncluded`

:relatedLot:
    string

    Id of related :ref:`lot`.

:date:
    string, :ref:`date`, autogenerated

:participationUrl:
    url

    A web address for participation in auction.

Workflow
--------

.. graphviz::

    digraph G {
        A [ label="pending*" ]
        B [ label="active"]
        C [ label="cancelled"]
        D [ label="unsuccessful"]
        E [ label="deleted"]
        F [ label="invalid"]
         A -> B [dir="both"];
         A -> C;
         A -> D [dir="both"];
         A -> E;
         A -> F [dir="both"];
         B -> C;
         D -> C;
         E -> C;
         F -> C;
         F -> E;
    }

\* marks initial state
