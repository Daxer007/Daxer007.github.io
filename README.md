<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Friendly Wellness Assistant - Workout Page</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <style>
        /* Custom styles go here */
        .remove-activity {
            display: none;
            color: red;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-center">Friendly Wellness Assistant</h1>
        <p class="text-center">Current Date: <span id="current-date"></span></p>
        <form id="workout-form">
            <div class="form-group">
                <label for="workout-activity">Select Workout Activity:</label>
                <select class="form-control" id="workout-activity">
                    <option value="">Select an activity</option>
                    <option value="Squats">Squats</option>
                    <option value="Push-ups">Push-ups</option>
                    <!-- Add more activity options here -->
                </select>
            </div>
            <div class="workout-control">
                <input type="text" id="new-activity" class="form-control" placeholder="Add a new activity">
                <button type="button" id="add-activity-btn" class="btn btn-primary">Add</button>
            </div>
            <ul class="workout-checklist">
                <!-- Selected activities will be added dynamically here -->
            </ul>
            <div id="fitness-graphics" class="carousel slide" data-ride="carousel">
                <!-- Fitness graphics carousel goes here -->
            </div>
            <div class="workout-routine">
                <h2>Workout Routine</h2>
                <ul>
                    <li>Warm-up: 5 minutes of light cardio</li>
                    <li>Strength Training: 3 sets of 10 reps for each exercise</li>
                    <ul>
                        <li>Squats</li>
                        <li>Push-ups</li>
                        <li>Lunges</li>
                        <li>Plank</li>
                    </ul>
                    <li>Cardio: 20 minutes of moderate-intensity exercise</li>
                    <li>Cool-down: 5 minutes of stretching</li>
                </ul>
            </div>
            <a href="orders.html" id="orders-link" class="btn btn-primary">Go to Orders Page</a>
        </form>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        // JavaScript/jQuery code goes here
        $(document).ready(function() {
            var selectedActivities = [];

            $('#workout-activity').change(function() {
                var selectedActivity = $(this).val();
                if (selectedActivity) {
                    selectedActivities.push(selectedActivity);
                    updateChecklist();
                }
            });

            $('#add-activity-btn').click(function() {
                var newActivity = $('#new-activity').val();
                if (newActivity) {
                    selectedActivities.push(newActivity);
                    updateChecklist();
                    $('#new-activity').val('');
                }
            });
            

            $(document).on('mouseenter', '.workout-checklist li', function() {
                $(this).find('.remove-activity').show();
            });

            $(document).on('mouseleave', '.workout-checklist li', function() {
                $(this).find('.remove-activity').hide();
            });

            $(document).on('click', '.remove-activity', function() {
                var index = $(this).data('index');
                selectedActivities.splice(index, 1);
                updateChecklist();
            });

            function updateChecklist() {
                var checklist = $('.workout-checklist');
                checklist.empty();
                selectedActivities.forEach(function(activity, index) {
                    var listItem = $('<li>').text(activity);
                    var removeButton = $('<span>').text('X').addClass('remove-activity').data('index', index);
                    listItem.append(removeButton);
                    checklist.append(listItem);
                });
            }

            $('#orders-link').click(function(event) {
                event.preventDefault();
                window.location.href = 'orders.html';
            });
        });
    </script>
</body>
</html>
