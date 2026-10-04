# pomegranate-shared-list

The public, account-free "view" page for a shared Pomegranate shopping
list or recipe. Hosted on GitHub Pages.

A Pomegranate user taps **Share** on a shopping list or a recipe, which
generates an unguessable token server-side (Supabase, `share_shopping_list()`
or `share_recipe()`). The resulting link looks like:

```
https://<this-site>/?list=<token>
https://<this-site>/?recipe=<token>
```

Anyone with that link can view the list (and tick items off) or the
recipe — no Pomegranate account needed, and no other app functionality is
exposed. Access is scoped entirely by narrow `SECURITY DEFINER` Postgres
functions (`get_shared_list`, `toggle_shared_item`, `get_shared_recipe`)
defined in the main app's `app/supabase/schema.sql` — this page's Supabase
key is the public `anon`/publishable key and carries no special privilege
on its own.

This is a single static `index.html` — no build step, no dependencies to
install. Edit it directly and push to `main`; GitHub Pages redeploys
automatically.
