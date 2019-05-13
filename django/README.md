## Django guidelines

### Use the name of the model, rather than the model object itself:
For models foreign keys use string format (`app.Model`) instead of actually importing the models. This will reduce
the probability of circular imports.

If the foreign key is in the same model file then mention the name of the model in string without app name (`Model`).

**Example:**

```
class UserProfile(models.Model):
    user = models.OneToOneField('User', on_delete=models.CASCADE, related_name="user_profile")
```

## Atomic increments/decrements

```
from django.db.models import F

Blog.objects.all().update(posts_count=F('posts_count') + 1)
```

This will update the count of posts in a blog atomically. This increments happens in the database and not at the application
level. If done at the app level, there might be issues with the count. Like 2 threads might read the post count as 1 and 
update the count 2, whereas it should've been 3.


## Merge querysets from same model

To merge 2 or more querysets, we can use boolean or to merge them into one single queryset. This is better than converting 
them to lists and extending them, since converting to lists makes database calls.

```
blog = Blog.objects.get(name='Django Blog')
user = User.objects.get(username='vitor')

django_stories = blog.stories.all()
vitor_stories = user.stories.filter(category__name='django')

stories = django_stories | vitor_stories  # merge querysets
```

## Django app naming

The name of the django apps should be singular. For example `user`, `event`.
