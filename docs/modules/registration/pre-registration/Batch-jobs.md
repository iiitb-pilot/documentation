# Batch Job Services

## Batch Jobs

Three batch jobs run in Pre-registration based on a cron scheduler.

## Consumed Status Batch Job

This batch job identifies the pre-registrations for which registration packets are created and are under processing in the server. The details about this pre-registration are removed from the pre-registration database and are moved to an archival table in pre-registration called consumed tables. Later the data in the consumed tables can be archived or removed based on the adopter's need.

## Expired Status Batch Job

This batch job identifies the pre-registrations which have expired and updates the status of these pre-registrations as "Expired".

## Booking Batch Job

Booking batch job runs every day to perform some standard tasks:

1. Creating the booking slots (if not available) for the next 140 days (configurable) using the details available for the centers like, center working hours, lunch breaks, no. of Kiosks, slot booking times & holidays.

2. Canceling bookings & sending notifications to the residents, if any emergency holiday has been declared for a center.

## To Do
## API Details
 * [API Documentation](Pre-Reg-API-Documentation.md)

* Configuration Parameters
    * List of parameters and how they alter the behaviour of the API

## Links to related content
* Link to design documentation,
* Links to How To articles
