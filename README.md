# Conference Management System Project in Django with Source Code

The **Conference Management System in Django** created based on **Python**, **Django**, and **SQLITE3 Database**.

The **Conference Management System** have the authority to organize new conferences, accept or reject submitted abstracts and papers, and assign abstracts and articles to reviewers.

Authors can submit abstracts and papers to conferences by uploading them.

They receive input from reviewers and make changes to their articles as needed.

A Conference Management System in Django is an easy project for beginners to learn how to build a web-based python Django project.

We will provide you with the complete source code and database for the python project so that you can easily install it on your machine and learn how to program in Python Django.

>[!NOTE]
> To start creating a **Conference Management System Project in Python Django**, makes sure that you have PyCharm Professional IDE Installed in your computer.

## Admin Features

* **Login Page**

The page where the system administrator enters their system credentials in order to gain access to the system’s administrative side.

* **Manage authors**

This is the page where an administrator can add, update, view and delete authors information.

* **Manage chairs**

This is the page where an administrator can add, update, view and delete chairs information.

*  **Conference Management**

This is the page where an administrator can add, update, view and delete conference information.

*  **Manage papers**

This is the page where an administrator can add, update, view and delete papers information.

* **Manage reviewers**

This is the page where an administrator can add, update, view and delete reviers information.

* **New User Page**

The page where a new admin credentials are created by an admin.

* **Users list**

This is the page that lists and manages the added users.


## How to Create a  Conference Management System in Django?

Here are the steps on how to create a **Conference Management System in Django** with Source Code.

1. **Open file.**

Open “pycharm professional” after that click “file” and click “new project”.

![image](https://github.com/user-attachments/assets/7bfec92a-7649-41af-b69c-d910ad14cd86)

2. **Choose Django**.

After click “new project“, choose “Django” and click.

3. **Select file location**.

Then, select a file location wherever you want.

 4. **Create application name**.

After that, name your application.

5. **Click create**.

Finish creating the project by clicking “create” button.

![image](https://github.com/user-attachments/assets/34ab0684-6106-44a2-a2af-5ac1650a682c)


6. **Start Coding**.

Finally, we will now start adding functionality to our Django Framework by adding some functional codes.

## Functionality and Codes

* Create template for the add conference form in Conference Management System in Django.

In this section, we will learn on how create a templates for the add conference form. 

To start with, add the following code in your conference.html under the folder of /templates/.

``` {%extends "upper_menu.html" %}
{% block head %}
    {% load static from staticfiles %}
    <link rel="stylesheet" href="{% static '/css/style_conference.css' %}">
{% endblock %}
{% block content %}
    <div id="divPaperMainContainer">
        <div id="divPaperListContainer" class="divChildHalfSpace">
            <table cellspacing="10">
                <tr>
                    <th>
                        Name
                    </th>
                    <th>
                        Status
                    </th>
                    <th>
                        Author
                    </th>
                    <th>
                        Author email
                    </th>
                    {% if chair_hashed_user_type == user_type %}
                    <th>
                        Assign to a Reviewer
                    </th>
                    {% endif %}
                    {% if chair_hashed_user_type == user_type %}
                    <th>
                        See review
                    </th>
                    {% endif %}
                    {% if chair_hashed_user_type == user_type %}
                    <th>
                        Accept
                    </th>
                    {% endif %}
                    {% if chair_hashed_user_type == user_type %}
                    <th>
                        Reject
                    </th>
                    {% endif %}
                </tr>
                {% for submit in submits %}

                        <tr>
                            <td>
                                {{ submit.0.paper.name }}
                            </td>
                            <td>
                                    <p style="border-radius:10px;color:#fff;background:{% if submit.0.submit_status in pending %}
                                        #777;
                                        {% endif %}

                                        {% if submit.0.submit_status in rejected %}
                                        #af1e01;
                                        {% endif %}
                                            {% if submit.0.submit_status in accepted %}
                                        #229954;
                                        {% endif %}">


                                {{ submit.0.submit_status }}
                                    </p>

                            </td>
                            <td>
                                {{ submit.0.author.name }}
                            </td>
                            <td>
                                <a href="mailto:{{ submit.0.author.email }}">email</a>
                            </td>
                            {% if chair_hashed_user_type == user_type %}
                            <td>
                                <a href="assign_paper?paper_id={{ submit.0.paper.id }}&conf_name={{ conf_name }}">Assign</a>
                            </td>
                            {% endif %}
                            {% if chair_hashed_user_type == user_type %}
                            <td>
                                <a href="paper_reviews?paper_id={{ submit.0.paper.id }}">See reviews</a>
                            </td>
                            {% endif %}
                            <td>
                            {% if chair_hashed_user_type == user_type and submit.0.submit_status not in accept_strings %}
                                {% if submit.1 %}
                                <a style="background: #4CAF50 " href="accept_reject_paper?is_accepted=True&submit_id={{ submit.0.id }}&conf_name={{ conf_name }}">Accept</a>
                                    {% else %}
                                    <p>Author has not uploaded a paper yet.</p>
                                {% endif %}
                            {% endif %}
                            </td>
                            <td>
                            {% if chair_hashed_user_type == user_type and submit.0.submit_status not in reject_strings %}
                                {% if submit.1 %}
                                <a style="background: #af1e01 " href="accept_reject_paper?is_accepted=False&submit_id={{ submit.0.id }}&conf_name={{ conf_name }}">Reject</a>
                                {% endif %}
                            {% endif %}
                            </td>

                        </tr>


                {% endfor %}
            </table>

        </div>
        <div id="divPaperSubmitContainer" class="divChildHalfSpace">
            {% if user_type == author_hashed_user_type%}
            <form id="formSubmitPaper" action="submit_paper" method="post">
            {% csrf_token %}
                <div class="divInputContainer"><p>Name : </p>
                    <select name="paper_id">
                        {% for paper in available_papers %}
                            <option value="{{ paper.id }}">{{ paper.name }}</option>
                        {% endfor %}
                    </select>
                </div>
                <input type="hidden" name="conf_name" value="{{ conf_name }}">
                <button id="buttonFormAddConference" type="submit">Submit Paper</button>
            </form>
            {% endif %}

        </div>

    </div>
{% endblock %}
```


* Create template for the add authors form in Conference Management System in Django.

In this section, we will learn on how create a templates for the add authors form. 

To start with, add the following code in your author_paper.html under the folder of /templates/.

``` {%extends "upper_menu.html" %}
{% block head %}
    {% load static from staticfiles %}
    <link rel="stylesheet" href="{% static '/css/style_conference.css' %}">
    <link rel="stylesheet" href="{% static '/css/style_general.css' %}">


{% endblock %}
{% block content %}
    <div id="divPaperMainContainer">
        <div id="divPaperListContainer" class="divChildHalfSpace">
            <table cellspacing="10">
                <tr>
                    <th>
                        Name
                    </th>
                    <th>
                        Status
                    </th>
                    <th>
                        Conference
                    </th>
                    <th>
                        Submit Date
                    </th>
                    <th>
                        Submit Status
                    </th>
                    <th>
                        Upload date
                    </th>
                </tr>
                {% for paper_submit in papers_submits %}

                        <tr>

                            <td>
                                <a href="paper?paper_id={{ paper_submit.0.id }}">{{ paper_submit.0.name }}</a>
                            </td>
                            <td>
                                {{ paper_submit.0.status }}
                            </td>
                            <td>
                                {% if paper_submit.1 %}
                                {{ paper_submit.1.conference.name }}
                                {% endif %}
                            </td>
                            <td>
                                {% if paper_submit.1 %}
                                {{ paper_submit.1.submit_date }}
                                {% endif %}
                            </td>
                            <td>
                                {% if paper_submit.1 %}
                                    <p style="border-radius:10px;color:#fff;background:{% if paper_submit.1.submit_status in pending %}
                                        #777;
                                        {% endif %}

                                        {% if paper_submit.1.submit_status in rejected %}
                                        #af1e01;
                                        {% endif %}
                                            {% if paper_submit.1.submit_status in accepted %}
                                        #229954;
                                        {% endif %}">


                                {{ paper_submit.1.submit_status }}
                                    </p>
                                {% endif %}
                            </td>
                            <td>
                                {{ paper_submit.0.upload_date }}
                            </td>

                        </tr>


                {% endfor %}
            </table>

        </div>
        <div id="divPaperAddContainer" class="divChildHalfSpace">
            <form action="add_paper_handle" method="post" enctype="multipart/form-data">
            {% csrf_token %}
                <div class="divInputContainer"><p>Name : </p><input type="text" placeholder="name" name="name"></div>
                <div class="divInputContainer"><p>Your abstract file : </p><input type="file" name="abstract_file" ></div>
                <input type="submit" value="Okay!">
            </form>
        </div>
    </div>
    <script src="{% static '/js/jquery-3.4.1.min.js' %}"></script>
    <script src="{% static '/js/js_conferences.js' %}"></script>
{% endblock %}

 ```


### 📌Here's the full documentation for the [Conference Management System Project in Django](https://itsourcecode.com/free-projects/django/conference-management-system-project-in-django-with-source-code/)
