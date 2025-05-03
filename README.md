<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>VIP Grammar Correction Platform</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
        }
        .vip-label {
            font-weight: bold;
        }
        .container {
            max-width: 900px;
        }
    </style>
</head>
<body>
<div class="container py-5">
    <h1 class="mb-4 text-center">📝 VIP Grammar Correction Platform</h1>

    <form method="post" class="card p-4 shadow-sm bg-white">
        <div class="mb-3">
            <label for="text" class="form-label">Enter your English text:</label>
            <textarea class="form-control" id="text" name="text" rows="6" required>{{ user_input }}</textarea>
        </div>

        <div class="mb-3">
            <label for="vip_level" class="form-label">Select VIP Level:</label>
            <select class="form-select" name="vip_level" id="vip_level">
                {% for level in vip_levels %}
                    <option value="{{ level }}" {% if selected_level == level %}selected{% endif %}>{{ level }}</option>
                {% endfor %}
            </select>
        </div>

        <div class="d-grid">
            <button type="submit" class="btn btn-primary">Check Grammar</button>
        </div>
    </form>

    {% with messages = get_flashed_messages(with_categories=true) %}
        {% if messages %}
            <div class="mt-3">
                {% for category, message in messages %}
                    <div class="alert alert-{{ category }} alert-dismissible fade show" role="alert">
                        {{ message }}
                        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                    </div>
                {% endfor %}
            </div>
        {% endif %}
    {% endwith %}

    {% if result %}
        <div class="mt-4">
            <h4>🛠 Suggestions:</h4>
            <ul class="list-group">
                {% for suggestion in result %}
                    <li class="list-group-item">{{ suggestion }}</li>
                {% endfor %}
            </ul>
        </div>
    {% endif %}

    {% if rewritten %}
        <div class="mt-4">
            <h4>✨ Rewritten Text (Platinum):</h4>
            <div class="card card-body bg-light">
                {{ rewritten }}
            </div>
        </div>
    {% endif %}

    <footer class="text-muted text-center mt-5">
        <hr>
        <p>&copy; {{ time.year }} VIP Grammar Correction Platform. All rights reserved.</p>
    </footer>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
