# Natural Language Processing of Aviation Occurrence Reports for Safety Management

## Datasets
### ASRS
|Human Factors             |                          |
|:-------------------------|-------------------------:|
| Communication Breakdown  | Physiological - Other    |
| Confusion                | Situational Awareness    | 
| Distraction              | Time Pressure            |
| Fatigue                  | Training / Qualification |
| Human-Machine Interface  | Troubleshooting          |
| Other / Unknown Workload |                          |

Distribution of human factors:

![freq_asrs](img/freq_hf.png)


### CADORS
|Occurrence Categories                                                 |                            |
|:---------------------------------------------------------------------|----------------------------|
| ATM/CNS                                                              | Ground handling            |
| Abnormal runway contact                                              | Icing                      |
| Abrupt manoeuvre                                                     | Loss of control - ground   |
| Aerodrome                                                            | Loss of control - inflight |
| Airprox/TCAS alert/loss of separation/(near)midair collisions        | Medical                    |
| Bird                                                                 | Navigation Errors          |
| Cabin safety events                                                  | Runway Incursion           |
| Collision with obstacle(s) during take-off or landing whilst airborne|  Runway excursion          |
| Controlled flight into or toward terrain                             | Runway incursion - animal  |
| Fire/smoke (non-impact)                                              | Security related           |
| System/component failure or malfunction [non-powerplant]             | Fuel related               |
| System/component failure or malfunction [powerplant]                 | Ground collision           | 
| Turbulence encounter                                                 | Undershoot/overshoot       |
| Wind shear or thunderstorm                                           |                            |

Distribution of occurrence categories:

![freq_cadors](img/occ_fq.png)

## Additional baselines for the task of automatic report categorization.

ASRS:
![ASRS](img/classification_ASRS.png)

CADORS:
![Cadors](img/classification_CADORS.png)

## Hyperparameters

### Automatic report categorization

Maybe Georgios can add something here? (optional)

### Topic modeling

Preprocessing:
- NLTK tokenizer
- NLTK wordnet lemmatizer
- numbers removed 
- trailing characters removed (e.g. 's)
- filter extremes
    - leave out words that occur in less than 20 documents
    - leave out words that occur in more than half of the documents

Model hyperparameters:
- implementation: Python Gensim
- number of topics = 40
- chunksize = 2000
- passes = 20
- iterations = 400
- alpha = 'auto' (learns an asymmetric prior from the corpus)
- eta = 'auto' (learns an asymmetric prior from the corpus)


### Automatic summary generation

- architecture: BART-large
- max input length = 1024 tokens
- training batch size = 1
- eval batch size = 1
- optimizer: AdamW
- learning rate \alpha = 5E-5
- top-k sampling = 50
- top-p sampling = 0.95
- early stopping after 3 epochs

## Additional / example results

### Automatic report categorization 

Maybe Georgios can add something here? (optional)

### Topic modeling
Topics:
| Topic Number | Top-10 Topic Words | Topic Quality
|:---|------------------------------------------------------------------------------------|-----|
| 1 | go, around, runway, tailwind, touchdown, anomaly, landing, proper, point, attempted | good |
| 2 | landing, gear, hard, nose, main, right, left, collapse, damage, resulting | good |
| 3 | flight, instructor, action, delayed, remedial, student, inadequate, non, input, hover | good |
| 4 | wire, glider, fence, out, transmission, their, route, allowed, effect, testing | poor |
| 5 | decision, improper, his, attempt, planning, off, flight, land, take, tailwind | good |
| 6 | which, resulted, an, with, subsequent, airplane, flight, collision, loss, impact | good |
| 7 | from, clearance, maintain, maneuver, while, altitude, tree, line, terrain, adequate | good |
| 8 | descent, off, aborted, rate, speed, uncontrolled, sign, strike, too, minimum | good |
| 9 | procedure, follow, being, for, operator, between, without, operating, incident, forward | good |
| 10 | landing, improper, flare, student, bounced, recovery, from, inadequate, supervision, misjudged | good |
| 11 | system, or, fire, malfunction, emergency, level, insufficient, conduct, electrical, injury | poor |
| 12 | associated, pressure, airstrip, induced, end, near, departure, with, becoming, is | poor |
| 13 | avoid, visual, see, continued, traffic, pattern, obstruction, inadvertently, his, area | good |
| 14 | a, result, separation, incorrect, rudder, up, assembly, her, under, rule | poor |
| 15 | runway, takeoff, after, any, on, instruction, abort, receiving, snow, adequately | poor | 
| 16 | during, control, maintain, landing, directional, airplane, roll, loss, takeoff, aircraft | good |
| 17 | fatigue, due, propeller, blade, engine, separation, from, fracture, bearing, crankshaft | good |
| 18 | engine, for, reason, loss, power, undetermined, carburetor, total, partial, due | good |
| 19 | approach, proper, on, final, path, land, while, time, altitude, sun | good |
| 20 | that, not, be, could, determined, no, bird, ditch, had, variable | good |
| 21 | aerodynamic, high, altitude, performance, density, weight, terrain, airplane, climb, exceeding | good |
| 22 | landing, forced, for, terrain, suitable, lack, wa, factor, precautionary, initiation | good |
| 23 | fuel, engine, power, loss, starvation, due, oil, line, total, improper | good |
| 24 | terrain, attack, unsuitable, landing, area, selection, cruise, for, soft, encountered | good |
| 25 | over, use, brake, excessive, application, improper, water, complete, onto, improperly | good |
| 26 | condition, flight, into, instrument, weather, meteorological, terrain, disorientation, spatial, night | good |
| 27 | wa, contributing, accident, factor, were, lack, by, airplane, his, experience | good |
| 28 | before, properly, that, prior, ensure, checklist, secure, door, preflight, his | good |
| 29 | condition, wind, crosswind, for, inadequate, compensation, gusty, gust, vehicle, evaluation | good |
| 30 | helicopter, rotor, tail, main, passenger, impairment, autorotation, rpm, due, practice | good |
| 31 | night, light, command, condition, not, field, dark, glidepath, by, maintained | good |
| 32 | while, at, low, altitude, maneuvering, angle, turn, taxi, mechanical, known | good |
| 33 | because, encounter, normal, precluded, flight, turbulence, crew, hydraulic, training, cause | poor |
| 34 | did, not, when, airport, available, he, on, air, information, controller | good |
| 35 | stall, airspeed, inadvertent, maintain, adequate, an, climb, initial, spin, loop | good |
| 36 | maintenance, inadequate, by, personnel, wing, inspection, improper, flap, lookout, visual | good |
| 37 | engine, power, loss, due, partial, cylinder, no, rod, valve, bolt | good |
| 38 | excursion, it, operation, have, would, led, following, pitch, reveal, installation | poor |
| 39 | fuel, engine, power, loss, exhaustion, inadequate, preflight, due, examination, planning | good |
| 40 | gusting, both, also, cable, causal, throttle, other, mechanic, compensate, rollover | poor |

### Automatic summary generation

Random sample of input - output text pairs and the text generated by the model, from the test set.

Input text 1:

On January 31, 2001, about 1315 Alaska standard time, a Douglas DC-6B airplane, N4390F, sustained substantial damage during landing at the Donlin Creek Airstrip, a remote mine site located about 12 miles north of Crooked Creek, Alaska. The airplane was being operated as a visual flight rules (VFR) cargo flight under Title 14, CFR Part 125, when the accident occurred. The airplane was registered to and operated by Everts Air Fuel, Inc., Fairbanks, Alaska. The two certificated airline transport pilots, and the flight engineer, were not injured. Visual meteorological conditions prevailed, and a visual flight rules (VFR) flight plan was in effect. The flight originated at the Fairbanks International Airport, Fairbanks, about 1130. During a telephone conversation with the National Transportation Safety Board investigator-in-charge on February 2, the captain related that the purpose of the flight was to deliver about 4,800 gallons of fuel oil to the remote mining site. He said that the 5,400 feet long by 100 feet wide airstrip was situated within hilly, snow-covered terrain. He added that the airstrip has a 7 percent uphill grade. Flat light conditions existed at the airstrip, and light snow showers were present, with visibility reported at 2 miles. The captain stated that during final approach, as the airplane passed over the airstrip threshold, flat light conditions made it very difficult to discern where the airstrip surface was. He said that the initial touch down was "firm", but was thought to be within acceptable tolerances. Just after touchdown, the left wing broke free from the airplane at the wing to fuselage attach point. The airplane veered to the left, and off the left side of the runway. The captain said that the airplane's computed landing weight was 92,260 pounds. The certificated airline transport captain related that the purpose of the flight was to deliver about 4,800 gallons of fuel oil to the remote mining site. He said that the 5,400 feet long by 100 feet wide airstrip was situated within hilly, snow-covered terrain. He added that the airstrip has a 7 percent uphill grade. Flat light conditions existed at the airstrip, and light snow showers were present, with visibility reported at 2 miles. The captain stated that during final approach, as the airplane passed over the airstrip threshold, flat light conditions made it very difficult to discern where the airstrip surface was. He said that the initial touch down was "firm", but was thought to be within acceptable tolerances. Just after touchdown, the left wing broke free from the airplane at the wing to fuselage attach point. The airplane veered to the left, and off the left side of the runway. The captain said that the airplane's computed landing weight was 92,260 pounds.

Target text 1:

The flight crew's misjudged flare while landing. Factors associated with the accident were flat light conditions, snow-covered terrain, and an uphill runway grade.

Prediction 1:

The pilot's failure to maintain directional control of the airplane during landing. Factors in the accident were flat light conditions, and snow-covered terrain.


Input text 2:

According to the pilot, as he was about 50 feet above ground level on short final over the threshold, the right wing leading edge of the airplane struck several birds. There were no significant changes in how the flight controls felt on subsequent inputs, and the airplane landed without further incident. The pilot stated that the flight departed the airport about 10 minutes prior to the collision, and they were conducting touch-and-go takeoffs and landings in moderate crosswind conditions. He stated that there were no NOTAM's in place warning of birds in the immediate area of the airport, and he did not have time to maneuver away from the birds. 

Target text 2:

unexpected collision with birds on short final that damaged the airplane wing structure.

Prediction 2:

An in-flight collision with birds during final approach.


Input text 3:

On April 22, 2004, about 1640 Pacific daylight time, a Robinson R22B, N8492A, collided with terrain and rolled over while hovering at the Long Beach Airport, California. Pacific Coast Helicopters was operating the helicopter under the provisions of 14 CFR Part 91. The commercial pilot, who was a certified flight instructor, received minor injuries, and the one passenger was not injured; the helicopter sustained substantial damage. The personal local flight departed from the Long Beach about 1540. Visual meteorological conditions prevailed, and a flight plan had not been filed. In a written statement, the pilot reported that he was practicing pedal turns on the designated helicopter pads at the airport. After several uneventful turns, he maneuvered the helicopter into a hover about 5 feet above ground level (agl), facing in a westerly direction, which was conducive to headwind conditions. He applied pressure to the left pedal, in an effort to complete a left pedal turn. The helicopter rapidly turned to the left, and the pilot felt a strong wind from the right. After turning about 90 degrees, the pilot attempted to stop the left yaw by applying right pedal. The pilot lost control of the helicopter as it continued the left turn another 360 degrees. The helicopter impacted the pad, and came to rest on its left side. The pilot reported no mechanical problems with the helicopter prior to the accident. The wind conditions reported by the Long Beach Aviation Routine Weather Report (METAR) at 1627, were 300 degrees at 16 knots. The helicopter collided with terrain and rolled over while hovering. While practicing pedal turns on the designated helicopter pads at the airport, the helicopter encountered gusty winds. The pilot lost control of the helicopter, and it impacted the ground, coming to rest on its left side. The pilot reported no mechanical problems with the helicopter prior to the accident. The wind conditions reported by the Long Beach Aviation Routine Weather Report (METAR) at 1627 were 300 degree at 16 knots.

Target text 3:

the pilot's inadequate compensation for gusty wind conditions and failure to maintain control of the helicopter while hovering.

Prediction 3:

the pilot's inadequate compensation for the gusty wind conditions, which resulted in a loss of tail rotor effectiveness and subsequent collision with terrain.


Input text 4:

On February 5, 1996, at 1415 eastern standard time, a Cessna 180D, N6423X, was substantially damaged during a forced landing after takeoff from the Islesboro Airport, Islesboro, Maine. The private pilot and passenger were not injured. Visual meteorological conditions prevailed for the personnel flight that originated at Islesboro, at 1410. No flight plan had been filed for the flight conducted under 14 CFR Part 91. In the NTSB Form 6120.1/2, the pilot stated that the pre-flight and engine run-up were normal. He departed from runway 19 at the Islesboro Airport (57B), and at approximately 500 feet above the ground, the airplane's engine began to run rough. The pilot initiated a right turn back to the airport, and the engine continued to run rough while the airplane climbed to 800 feet. This was followed by a complete loss of engine power as the airplane was approaching runway 01. The pilot further stated: "...Intersected runway at 45 degree, descending, no power, with tailwind of 10 knots. Very difficult...to make left turn northbound to rwy 1. Nearly hit tree tops on east side of runway, was just regaining control...when engine gave an unexpected burst of power. This changed my mind to think of flying out to the water and landing on the frozen...bay...but power lasted perhaps 4 seconds, enough to gain 50 feet of altitude so that we were able to miss several power lines and fly, mush, into the tops of a stand of [trees]..." The airplane then collided with trees about 1/4 mile north of the runway. According to the Federal Aviation Administration (FAA) Inspector's report, a witnesses observed black smoke coming from the engine during the airplane's return to the airport. Examination of the engine and the fuel system revealed, "...No direct evidence to establish the reason for the engine exhausting black smoke during this event..." The pilot/owner stated that the preflight and engine run-up were normal, and he departed from runway 19 which is 2400 feet long. At approximately 500 feet above the ground, the airplane's engine began to run rough. The pilot reversed course to make a forced landing on runway 1 with a 10 knot tailwind. The engine subsequently lost complete power; however, a burst of power occurred afterwards. According to the pilot, the airplane overshot the runway. He avoided power lines, and then the aircraft 'mushed' into trees about 1/4 mile north of the runway. A witnesses observed black smoke coming from the engine during the airplane's return to the airport. Examination of the engine and the fuel system revealed no evidence of malfunction.

Target text 4:

a loss of engine power for an undetermined reason.

Prediction 4:

loss of engine power for undetermined reason(s). The lack of suitable terrain for a forced landing was a related factor.


Input text 5:

On June 20, 1994, at 1730 central daylight time, a Grumman G-164B, N112JM, was substantially damaged near Brinkley, Arkansas, following a total loss of engine power during takeoff. The commercial pilot did not receive injuries. Visual meteorological conditions prevailed for the local aerial application flight. During telephone interviews, the pilot and operator reported an "abnormal engine noise" occurred as the airplane crossed the departure end of the runway. The pilot dumped the load, cleared trees, and maintained level flight. The pilot said "the engine coughed and black smoke rolled from it." A witness also observed black smoke from the airplane. The pilot executed a forced landing into an adjacent rice field. During the landing roll, the main gear hit a rice levee and the airplane nosed over to an inverted position and slid into another rice levee before coming to rest. The rudder, vertical stabilizer, and wing spars were damaged. During a telephone interview, a company mechanic stated that the reciprocating radial engine had 1,135 hours since the last overhaul. He further said the engine had between 9,000 and 10,000 total hours. The engine and accessories were examined on August 24, 1994, at Greenwood, Mississippi. The report is enclosed. The supercharger impeller P/N 12788 was damaged where the blades had contacted the housing. Impeller bearing P/N 288943 had failed. The airplane was released to the owner. during the takeoff initial climb smoke came from the engine and a power hesitation occured. the pilot dumped the load and turned the airplane toward the airport. as more smoke came from the engine, a total loss of power occurred. during the forced landing the airplane crossed a tree line and landed in a rice field. during the landing roll, the main gear hit a levee and the airplane came to rest inverted. examination of the engine and accerssories revealed the supercharger impeller p/n 12788 was damaged where the blades had contacted the housing. the impeller bearing p/n 288943 had failed and allowed the impeller to be destroyed resulting in a complete loss of the engine power.

Target text 5:

a supercharger impeller bearing failure. a factor was the lack of suitable terrain for the forced landing.

Prediction 5:

the failure of the supercharger impeller bearing which resulted in a total loss of engine power. a factor was the lack of suitable terrain for the forced landing.


Input text 6:

the flt had been vectored for runway 13r by approach control from the point of initial contact. it was then handed off to tower; there was no verbal coordination between approach & tower. a military transport helicopter executed an approach to the same runway ahead of the accident airplane, and terminated at about a 300-ft hover over the runway. the pilot of the accident airplane requested vectors for separation; tower responded separation '...should be just fine....' shortly thereafter, while the airplane was over the threshold of runway 13r, the pilot requested confirmation that she was supposed to be behind the helicopter. the tower responded '...you were cleared to land on the left runway.' the pilot responded 'okay understand we were one three right.' as the airplane was flaring, it encountered vortex turbulence from the helicopter and control was lost. the tower never issued the accident airplane a landing clearance to either runway, nor was a clearance to land requested by the pilot.

Target text 6:
the approach controller's failure to properly sequence arriving traffic, and the tower controller's failure to sequence and separate landing traffic. factors in the accident were: the pilot's failure to obtain a landing clearance and the night light conditions.

Prediction 6:
the pilot's failure to maintain control of the helicopter, resulting in an encounter with vortex turbulence. factors related to the accident were: the pilot's improper use of the flight controls, and the failure of the tower to provide a safety advisory.
