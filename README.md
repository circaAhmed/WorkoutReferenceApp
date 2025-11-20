# 💪 Workout Reference App

A mobile-first exercise reference app designed to be your gym companion. Quick access to 47 pre-loaded exercises organized by body part with detailed information for each movement.

## Features

### 📱 **Mobile-Optimized Design**
- Large, tappable buttons (44px+ touch targets)
- Smooth expand/collapse animations
- Sticky header with filters always accessible
- Optimized for one-handed use
- Fast loading, no lag

### 🎯 **Smart Filtering System**

**Primary Filter - Upper/Lower Body:**
- Toggle between Upper Body and Lower Body exercises
- Updates available body part filters dynamically

**Secondary Filter - Body Part:**
- **Upper Body**: Chest, Back, Shoulders, Biceps, Triceps
- **Lower Body**: Quads, Hamstrings, Glutes
- Filter to specific muscle groups

**Additional Filter - Objective:**
- **💪 Strength**: Mass-building and strength-focused exercises
- **🔄 Rehab**: Mobility, stability, and rehabilitation movements
- **All**: View everything

### 📋 **Exercise Library**

**47 Pre-loaded Exercises:**
- **Chest**: 6 exercises (Bench Press, Incline Press, Flyes, etc.)
- **Back**: 6 exercises (Pull-ups, Rows, Deadlifts, etc.)
- **Shoulders**: 6 exercises (Overhead Press, Lateral Raises, etc.)
- **Biceps**: 5 exercises (Curls, Hammer Curls, etc.)
- **Triceps**: 6 exercises (Dips, Extensions, Pushdowns, etc.)
- **Quads**: 6 exercises (Squats, Lunges, Leg Press, etc.)
- **Hamstrings**: 6 exercises (RDLs, Leg Curls, etc.)
- **Glutes**: 6 exercises (Hip Thrusts, Bridges, etc.)

**Each Exercise Includes:**
- Exercise name
- Body part targeted
- Objective (Strength/Rehab)
- Detailed description
- Reference weight for intermediate-advanced lifters (assuming 3x8 rep range)
- Visual placeholder/icon

### 🎨 **Collapsible Card Design**

**Collapsed View (Default):**
- Exercise name
- Body part badge
- Objective badge (💪 Strength / 🔄 Rehab)
- Tap to expand

**Expanded View:**
- Full exercise details
- Visual illustration placeholder
- Complete description
- Reference weight and rep scheme
- Notes for intermediate-advanced lifters

## Installation

### Prerequisites
- Python 3.9+
- pip

### Setup

1. **Install dependencies:**
```bash
pip install -r requirements.txt
```

2. **Initialize database:**
```bash
python3 -c "from app import init_db; init_db()"
```

3. **Seed exercise database:**
```bash
python3 init_exercises.py
```

4. **Run the app:**
```bash
python3 app.py
```

5. **Open your browser or phone:**
```
http://localhost:5000
```

**For mobile testing:** Connect to your computer's local IP (e.g., `http://192.168.1.X:5000`)

## Usage Guide

### At the Gym

1. **Open the app** on your phone
2. **Select Upper or Lower Body** using the toggle at top
3. **Filter by body part** (e.g., tap "Chest" for chest day)
4. **Optionally filter by objective** (Strength vs Rehab)
5. **Scroll through the exercise list**
6. **Tap any exercise** to expand and see:
   - Full description
   - Reference weights
   - Visual illustration

### Example Workflow

**Chest Day:**
1. Tap "Upper Body"
2. Tap "Chest"
3. See 6 chest exercises
4. Tap "Barbell Bench Press" to see details
5. Reference: "3x8 @ 135-225 lbs for intermediate-advanced"

**Leg Day - Glute Focus:**
1. Tap "Lower Body"
2. Tap "Glutes"
3. See 6 glute-focused exercises
4. Tap "Hip Thrusts" for form details

## File Structure

```
workout-app/
├── app.py                    # Flask backend with API
├── init_exercises.py         # Database seeder script
├── exercises.db             # SQLite database (auto-created)
├── requirements.txt          # Python dependencies
├── templates/
│   └── index.html           # Mobile-first single-page app
└── README.md
```

## Database Schema

```sql
CREATE TABLE exercises (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    body_part TEXT NOT NULL,              -- Chest, Back, Shoulders, etc.
    upper_lower TEXT NOT NULL,            -- Upper or Lower
    objective TEXT NOT NULL,               -- Strength or Rehab
    description TEXT NOT NULL,             -- One-line exercise description
    reference_weight TEXT NOT NULL,        -- e.g., "3x8 @ 135-225 lbs"
    image_placeholder TEXT                 -- Emoji/icon placeholder
);
```

## API Endpoints

- `GET /` - Main app page
- `GET /api/exercises` - Get exercises with optional filters
  - Query params: `upper_lower`, `body_part`, `objective`
- `GET /api/body-parts` - Get body part categories

### Example API Calls

```bash
# Get all upper body exercises
curl "http://localhost:5000/api/exercises?upper_lower=Upper"

# Get chest exercises only
curl "http://localhost:5000/api/exercises?upper_lower=Upper&body_part=Chest"

# Get lower body strength exercises
curl "http://localhost:5000/api/exercises?upper_lower=Lower&objective=Strength"
```

## Customization

### Adding More Exercises

Edit `init_exercises.py` and add exercises to the `exercises` list:

```python
('Exercise Name', 'Body Part', 'Upper/Lower', 'Strength/Rehab',
 'Description here', '3x8 @ weight range', '💪'),
```

Then re-run:
```bash
python3 init_exercises.py
```

### Changing Filters

Edit body part categories in `app.py`:

```python
upper_body = ['Chest', 'Back', 'Shoulders', 'Biceps', 'Triceps']
lower_body = ['Quads', 'Hamstrings', 'Glutes', 'Calves']  # Add Calves
```

## Tech Stack

- **Backend**: Flask (Python web framework)
- **Database**: SQLite (lightweight, file-based)
- **Frontend**: HTML5 + TailwindCSS
- **JavaScript**: Vanilla JS (no frameworks)
- **Mobile**: Responsive design, optimized for phones

## Mobile Optimization Features

- **Sticky Header**: Filters always accessible while scrolling
- **Touch Targets**: Minimum 44x44px for easy tapping
- **Smooth Animations**: Expand/collapse transitions
- **Large Fonts**: Readable without zooming
- **No Horizontal Scroll**: Everything fits on screen
- **Fast Performance**: Client-side filtering, no page reloads
- **Offline Capable**: Works after initial load (data cached)

## Tips

### Best Practices

1. **Bookmark on your phone** for quick access at the gym
2. **Use filters strategically** - Filter by body part to focus on today's workout
3. **Reference weights are guidelines** - Adjust based on your fitness level
4. **Tap to expand only when needed** - Collapsed view shows key info

### Progressive Overload

Use the reference weights as targets:
- **Below reference range**: Focus on form, gradually increase
- **At reference range**: You're intermediate-advanced
- **Above reference range**: You're advanced, consider higher rep ranges or intensity techniques

## Future Enhancements

Potential features to add:
- Personal workout logs
- Progress tracking over time
- Custom exercise additions
- Rest timer
- Workout templates/routines
- Form videos/GIFs
- Exercise variations
- Equipment alternatives

## License

Free to use and modify for personal use.

---

**Happy lifting!** 💪🏋️‍♂️

Open http://localhost:5000 on your phone and take it to the gym!