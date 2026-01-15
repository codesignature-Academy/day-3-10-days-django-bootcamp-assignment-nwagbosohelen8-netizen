[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/O1WLF7Qp)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=22246744&assignment_repo_type=AssignmentRepo)
# Django Views & URL Routing Assignment

## Assignment Overview
In this assignment, you will practice creating Django views and connecting them to URLs using the URL routing system. You'll create HTML templates and use anchor tags to navigate between different pages.

## Learning Objectives
- Create Django views and render HTML templates
- Configure URL routing in Django
- Use anchor tags to create navigation between pages
- Understand the relationship between views, URLs, and templates

---

## Setup Instructions

### Step 1: Clone the Repository
Clone the repository to your local machine:
```bash
git clone <repository-url>
```

### Step 2: Navigate to the Project Directory
Change into the project directory:
```bash
cd day-3-assignment
```

### Step 3: Install Dependencies
Install the required Python packages:
```bash
pip install -r requirements.txt
```

---

## Assignment Tasks

### Task 1: Create the Home Page

#### 1.1 Create `home.html` Template
- Location: `templates/home.html`
- Create a new `templates/` folder in the project root directory (same level as `manage.py`)
- Create a new file `home.html` inside the `templates/` folder in the project root directory
- Add basic HTML structure with a title "Home Page" and a welcome message
- Add an unordered list (`<ul>`) with anchor tags (`<a>`) that link to the three pages you'll create in Task 2

#### Example Structure:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Home Page</title>
</head>
<body>
    <h1>Welcome to Our Website</h1>
    <p>Choose a page to visit:</p>
    <ul>
        <li><a href="{% url 'page1' %}">Page 1</a></li>
        <li><a href="{% url 'page2' %}">Page 2</a></li>
        <li><a href="{% url 'page3' %}">Page 3</a></li>
    </ul>
</body>
</html>
```

### Task 2: Create the Home View Function

#### 2.1 Update `myapp/views.py`
- Create a `home()` view function that renders the `home.html` template
- Use `render()` function to return the HTML template

#### Example:
```python
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

### Task 3: Configure URLs

#### 3.1 Update `proj/urls.py`
- Import the `home` view from `myapp.views`
- Add a URL pattern for the home page using `path('', views.home, name='home')`

#### Example:
```python
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
]
```

### Task 4: Create Three Additional View Functions

Create three additional view functions in `myapp/views.py`. Each function should:
- Accept a `request` parameter
- Render a different HTML template
- Have a descriptive name (e.g., `page1()`, `page2()`, `page3()`)

#### 4.1 Create Template Files
Create three HTML template files in the `templates/` folder in the project root directory:
- `templates/page1.html`
- `templates/page2.html`
- `templates/page3.html`

Each template should:
- Have a title corresponding to its page number
- Include a "Back to Home" link that redirects to the home page using `{% url 'home' %}`
- Include some unique content to distinguish the pages

#### Example for `page1.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Page 1</title>
</head>
<body>
    <h1>This is Page 1</h1>
    <p>Welcome to Page 1. Add your content here.</p>
    <a href="{% url 'home' %}">Back to Home</a>
</body>
</html>
```

#### 4.2 Add View Functions
Add the three view functions to `myapp/views.py`:

```python
def page1(request):
    return render(request, 'page1.html')

def page2(request):
    return render(request, 'page2.html')

def page3(request):
    return render(request, 'page3.html')
```

#### 4.3 Add URL Patterns
Add URL patterns to `proj/urls.py`:

```python
path('page1/', views.page1, name='page1'),
path('page2/', views.page2, name='page2'),
path('page3/', views.page3, name='page3'),
```

### Task 5: Update Home Page Navigation

Ensure your `home.html` has anchor tags linking to all three pages using Django's URL template tag:
```html
<ul>
    <li><a href="{% url 'page1' %}">Go to Page 1</a></li>
    <li><a href="{% url 'page2' %}">Go to Page 2</a></li>
    <li><a href="{% url 'page3' %}">Go to Page 3</a></li>
</ul>
```

---

## Testing Your Work

### Step 1: Run the Development Server
```bash
python manage.py runserver
```

### Step 2: Open in Browser
Navigate to `http://localhost:8000/` in your web browser

### Step 3: Test Navigation
- Verify that the home page loads correctly
- Click on each anchor tag to navigate to page1, page2, and page3
- Click "Back to Home" on each page to return to the home page
- Ensure all links work correctly

---

## Submission Checklist

- [ ] `home.html` template created in `templates/` (project root)
- [ ] `page1.html`, `page2.html`, `page3.html` templates created in `templates/` (project root)
- [ ] `home()` view function created in `myapp/views.py`
- [ ] `page1()`, `page2()`, `page3()` view functions created in `myapp/views.py`
- [ ] All URL patterns added to `proj/urls.py` with proper names
- [ ] Home page displays all navigation links
- [ ] All anchor tags work and redirect correctly
- [ ] "Back to Home" links work on all pages
- [ ] No errors when running the development server

---

## Key Concepts

### Django Views
- Views are Python functions that receive a web request and return a web response
- They contain the logic for processing user requests and rendering templates

### URL Routing
- URL patterns map URLs to view functions
- The `path()` function defines a URL pattern with optional view and name parameters
- The `name` parameter allows you to reference URLs by name in templates using `{% url 'name' %}`

### Templates
- Templates are HTML files that Django renders with context data
- Use the `render()` function to combine a template with context and return an HTTP response
- Django's template language allows you to use tags like `{% url %}` to generate dynamic URLs

### Navigation with Anchor Tags
- Use `<a href="{% url 'name' %}">Link Text</a>` to create links between pages
- This approach ensures links work even if URLs change (only need to update in `urls.py`)

---

## Troubleshooting

**Issue: Template not found**
- Ensure `templates` folder is created at the project root (same directory as `manage.py`)
- Ensure the template file name matches exactly in the `render()` function

**Issue: URL not found (404 error)**
- Verify the view function is imported in `urls.py`
- Check that the URL pattern name matches the one used in the template

**Issue: Anchor tags not working**
- Use `{% url 'view_name' %}` syntax in templates, not hardcoded URLs
- Ensure all view functions are named and added to `urlpatterns` in `urls.py`

---

## Summary

By completing this assignment, you will have:
1. ✓ Created Django view functions
2. ✓ Rendered HTML templates from views
3. ✓ Configured URL routing in Django
4. ✓ Created dynamic navigation using anchor tags
5. ✓ Understood the MTV (Model-Template-View) architecture in Django

Happy coding! 🚀
