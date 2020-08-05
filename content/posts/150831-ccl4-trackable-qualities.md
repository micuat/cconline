+++
author = "Choreographic Coding Lab"
title = "CCL4: Trackable Qualities"
date = "2015-08-31"
description = "report"
tags = [ "ccl" ]
+++


Table of qualities
--------

Center of Mass

- Definition: A physics term, in this case meaning the center of mass for the performer. There can be lots of movement without any appreciable change in the position of the Center of Mass.

Bounding Box

- A rectilinear box in Cartesian space which is as small as possible while completely containing the performer. The axes of the box are basically arbitrary, but usually consistent for the duration of a piece.

Kinetic Sphere

- A sphere which is as small as possible while completely containing the performer. A closer approximation to the area of influence of the performer than the Bounding Box.

Reach

- the action of reaching, with an intended, distant point outside of the body, out of reach

Circularity

- Either the static form of pieces of the body in a circular arrangement (ie. arms is first position), or movement of a body part in circles.

Linear Quality of Form

- Similar to the opposite of Circularity. long lines, straight limbs as opposed to curves.
- Might be able to use "best fit" lines or curves to see how off a series of points is from a perfect line or curve, etc.
- On a spectrum between curvy and linear?
    - Three part continuum - linear or triangular? - between linear, angular, curvy

Linear Quality of Movement

- Linear Quality of Form over time

Level

- Performer's height from the floor. Example terms: Low, Medium, High, Lower, Higher.

Travel Intensity

- Space recently being used/activated by the performer. Travel Intensity would be higher while travelling across the room, and would be lower while dancing in one spot

Openness

- The amount to which a position or energy is extroverted or introverted, "turned-in" or "turned-out"

Stance / Contact Area

- Points of contact such as where your feet are, including point and area of contact.

Balance / Sturdiness

- A function of Center of Mass and Stance / Contact Area

Negative Space

- Created space, enclosed space, but not inhabited space. 
- Perhaps spheres within the Kinetic Sphere which do not contain body points

Avoided Space

- Space which is defined over time by the performer's avoidance of it.
- Possibly by building a heatmap of occupied space over the course of a performance we can uncover these avoided spaces.
    - using other information such as sudden changes in momentum, we could more clearly define the edges of this avoided space.

Texture of Movement

- Thick vs. Soft (from Gaga technique). A movement with lots of resistance, vs. free-flowing

Gaze

- Direction or point that performer is looking at

Parallelism

- The amount to which lines extended from particular body parts (such as the forearms) are parallel to one-another.

Joint Angles

- The angle between two connected body parts, such as the right upper arm and right fore arm.



Initiation of Movement

- Point (inside or outside of the body) from which a movement originates

Degree of Interruption

- Smoothness of movement. flowing movement vs. fragmented or interrupted movement

Groove

Alignments

- See: Linear Quality of Form?



…


Sensors
--------


- Blood Pressure
- Heart Rate
- ...



Axes
--------

One Attempt to Organize Qualities into Independent Axes

ENERGY

- Stability (balance)
- Scale (small circles versus big circles)
- Entropy (degree of disruption/chaos versus smoothness)
- Effort level (thickness/softness)
- Velocity graph (Acceleration-Decay-Sustain-Release + direction of movement)
- Rhythm (random versus clear pattern or groove)


WITHIN THE BODY

- Materiality (bone, muscle, skin)
- Locus of initiation
- Pathway (circular, linear, spiral)
- Entropy (degree of alignment / symmetry)
- Degree of openness/closeness (orientation + reach)


SPACE

- Orientation
- Level
- Pathway through space (circular, linear, spiral)
- Alignments / Symmetry
- Negative space (traveled space, claimed space, created/enclosed/carved space, vacated space, avoided space)



Data
--------

- Using mocap @ NYU
- 49 markers
- Not all markers are needed to find these qualities
- Reduce data by approximating
    - Hand position (Left and Right)
        - 2 markers per hand
        - 3 finger markers per hand
    - Foot position (Left and Right)
        - 3 markers per foot
    - Joint position
        - Wrists
        - Elbows
        - Shoulders
        - Ankles
        - Knees
        - Can this be output by the system or do we need to approximate these using the marker data?
- Best strategies for dealing with NULL values
- Ignore marker?
- Linear averaging between last and next known positions?
    - this might work for small holes in data (lasting only a frame or two), but probably not for larger gaps
- Allow for quality values between separate body parts
- (i.e. parallelity between Left Forearm and Right Lower Leg)

