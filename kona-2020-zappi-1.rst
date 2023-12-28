2020 Kona with 1st Gen Zappi
============================

These are the current versions that are being used to test:

.. list-table:: Kona versions
    :align: left

    * - Model
      - OSAE.S5BLC.AEU
    * - Software
      - OS_E_20.EUR.S5W_L.001.001.191223
    * - Firmware
      - OS_E_20.EUR.01.191122.MICOM

.. list-table:: Zappi firmware versions
    :align: left

    * - Hub
      - v3.077
    * - Zappi
      - v3.11.4
    * - Harvi
      - ???

Configurations
~~~~~~~~~~~~~~

The following configurations have been tested:

Eco+, Scheduled Boost on Zappi with no Scheduled Charge on Kona
---------------------------------------------------------------

*71% success rate (5/7 attempts)*

This is the configuration that should "just work" and is likely the preferred setup for most people.

Possible problems:

- :ref:`charge-delayed-no-start` *50% of failures (1/2 failures)*

- :ref:`charge-delayed-early-stop` *50% of failures (1/2 failures)*

.. _eco_plus_scheduled_boost_scheduled_charge:

Eco+, Scheduled Boost on Zappi with Scheduled Charge on Kona
------------------------------------------------------------

*Anecdotally this was fairly reliable until the second half of 2023*

The idea here is that because the Kona fails to wake when requested by the zappi,
if the Kona is also configured to wake independently of the zappi, then it'll be ready
to start charging when requested to do so by the zappi.

Possible problems:

- :ref:`charge-delayed-no-start`

.. _eco_scheduled_boost_scheduled_charge:

Eco, Scheduled Boost on Zappi with Scheduled Charge on Kona
-----------------------------------------------------------

*0% success rate (0/1 attempts)*

This should be a "safe fallback" for when a vehicle is really low on battery and you want
to ensure a charge. However, on the one attempt, the vehicle did charge at 1.4 kW
until the start of the timed boost and then :ref:`charge delayed <charge-delayed-early-stop>`
after around 1 hour of boosted charge.

Possible problems:

- :ref:`charge-delayed-early-stop` *100% of failures (1/1 failures)*

.. _fast_scheduled_charge:

Fast on Zappi with Scheduled Charge on Kona
-------------------------------------------

*50% success rate (1/2 attempts)*

This flips things around and should rely just on the car's charge schedule.
The drawback is that, during the summer, this would prevent charging the car with
excess solar, which is sort of the whole point of the zappi.

- :ref:`charge-delayed-early-stop` *100% of failures (1/1 failures)*

Problems
~~~~~~~~

.. _charge-delayed-no-start:

Scheduled Boost doesn't start with "Charge Delayed"
---------------------------------------------------

Here, the zappi is "Waiting for Surplus" when you plug the vehicle in and the overnight
scheduled boost does not occur at all. The zappi shows "Charge Delayed" in the morning.

Try:

- :ref:`eco_plus_scheduled_boost_scheduled_charge`.
- :ref:`fast_scheduled_charge`.
- :ref:`eco_scheduled_boost_scheduled_charge`.


.. _charge-delayed-early-stop:

Scheduled Boost stops early with "Charge Delayed"
-------------------------------------------------

Here, the zappi is either:

- "Waiting for Surplus" when you plug the vehicle in
- "Charging" when you plug the vehicle in, but at the minimum 1.4kW

The overnight scheduled boost starts, but then stops after 30-60 minutes.

The zappi shows "Charge Delayed" in the morning.

The Kona may show "Charging Interrupted. Please check the AC charger." when turned on.

Try :ref:`fast_scheduled_charge`.

.. _kona-holds-charge-cable:

Kona won't release the charging cable
-------------------------------------

This has been observed as a result of :ref:`charge-delayed-early-stop`.

If you try and press the car's power button with the break peddle depressed it will try the start
cycle again and complain that the charging cable is still plugged in.

Try :ref:`turn-kona-off-after-failed-turn-on`.

Kona stuck "on" but unable to start
-----------------------------------

You're pressed the power button but the Kona is unhappy about something.
Pressing the start button again just appears to do the same thing.


Try :ref:`turn-kona-off-after-failed-turn-on`.

Possible Solutions
~~~~~~~~~~~~~~~~~~

.. _turn-kona-off-after-failed-turn-on:

Turning Kona off when charging cable plugged in
-----------------------------------------------

You need to press the power button with your feet off any peddles to turn the car off.
You should then be able to pull the charging cable out.
