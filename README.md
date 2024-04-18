# office-fitness-bot
Automated exercise reminder for employees via slack.

Find the complete python script for the pipedream workflow automation below:
```
from datetime import datetime

# START: define constants

MESSAGE_TUESDAY = """Hello, it's *Tuesday* and the exercise session at *10:15* is coming up. :runner::man-lifting-weights:
Take a healthy 5 minutes off the task, do these exercises and come back stronger:

1. _Bench position - Diagonal arm & leg stretches_: per leg, 5x
2. _Lunges_: per leg, 10-15x (slightly but not totally exhausting)
3. _One-legged “key pickups”_: per leg, 3-5x
4. _Squats_: 5x

Detailed description <https://mopius.atlassian.net/wiki/spaces/MOP/pages/93192193/5-min+Office+Fitness#TUESDAY|here>. React with any emoji :white_check_mark: to mark the workout as completed.
I'm rooting for you!"""

DESC_TUESDAY = """
An optional, additional description for Tuesday.

"""

MESSAGE_WEDNESDAY = """Hello, it's *Wednesday* and the exercise session at *10:15* is coming up. :weight_lifter::woman-cartwheeling:
Get a healthy break, fuel your energy and be good to your body with these exercises:

1. _Seite-zu-Seite schwingen_: 10x each side
2. _“Bring-knee-to-front” hip flexor stretches_: per leg, 3x clockwise, 3x counter-clockwise
3. _One-legged table plank_: per leg, 5x clockwise and then 5x counter-clockwise
4. _Schifahr/Fußball-Beinschwingen_: per leg: 5x back/forth, 5x left/right
5. _Jumping squats_: 5x

Detailed description <https://mopius.atlassian.net/wiki/spaces/MOP/pages/93192193/5-min+Office+Fitness#WEDNESDAY|here>. React with any emoji :white_check_mark: to mark the workout as completed.
You got this!"""

DESC_WEDNESDAY = """
An optional, additional description for Wednesday.
"""

MESSAGE_DEFAULT = """
This should actually not happen. Anyway, happy working!
"""

# END: define constants

def handler(pd: "pipedream"):
    # Reference data from previous steps
    print(pd.steps["trigger"]["context"]["id"])
    # Return data for use in future steps
    # determine week day: 1 = Tuesday, 2 = Wednesday
    weekday = datetime.now().weekday()

    # initialize message as default message
    message = MESSAGE_DEFAULT
    desc = "Default description"

    if weekday == 1:
        message = MESSAGE_TUESDAY
        desc = DESC_TUESDAY
    elif weekday == 2:
        message = MESSAGE_WEDNESDAY
        desc = DESC_WEDNESDAY

    return {"workout": {"message": message, "desc": desc}}
```
