Toshiba IR Remote Climate
=========================

.. seo::
    :description: Controls a Toshiba WH-H01EE compatible Climate via IR
    :image: air-conditioner.png

The ``toshiba`` climate platform allows you to control a Toshiba WH-H01EE compatible heat pump by
sending IR signals as your remote unit would do.

This component requires that you have setup a :doc:`/components/remote_transmitter`.

Due to the unidirectional nature of IR remote controllers, this component cannot determine the
actual state of the device, and will assume the state of the device is the latest state requested.

Optionally you can add a :doc:`/components/remote_receiver` component so the climate state will be
tracked when it is operated with the original remote controller unit.

.. figure:: images/climate-ui.png
    :align: center
    :width: 60.0%

.. code-block:: yaml

    # Example configuration entry
    remote_transmitter:
      pin: GPIO32
      carrier_duty_percent: 50%

    climate:
      - platform: toshiba
        name: "Lounge Heat Pump"

Configuration variables:
------------------------

- **name** (**Required**, string): The name for the climate.
- **supports_cool** (*Optional*, boolean): Enables setting cool mode for this climate device. Defaults to ``True``.
- **supports_heat** (*Optional*, boolean): Enables setting heat mode for this climate device. Defaults to ``True``.
- **sensor** (*Optional*, :ref:`config-id`): The sensor that is used to measure the ambient
  temperature. This is only for reporting the current temperature in the frontend.
- **receiver_id** (*Optional*, :ref:`config-id`): The remote_receiver id, see: :ref:`toshiba-receiver_id`.
- All other options from :ref:`Climate <config-climate>`.

Advanced options:

- **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.
- **transmitter_id** (*Optional*, :ref:`config-id`): Manually specify the ID of the remote transmitter.

.. _toshiba-receiver_id:

Using a receiver
----------------

When using a receiver it is recommended to put the IR receiver as close as possible to the equipment's
IR receiver.

.. code-block:: yaml

    # Example configuration entry
    remote_receiver:
      id: rcvr
      pin:
        number: D4
        inverted: True
      tolerance: 40 # high tolerance required for some remote control units

    climate:
      - platform: toshiba
        name: "Lounge Heat Pump"
        receiver_id: rcvr

See Also
--------

- :doc:`/components/climate/index`
- :doc:`/components/remote_transmitter`
- :apiref:`toshiba/toshiba.h`
- :ghedit:`Edit`
