This repo is to show a bug in setTintList for TabLayout icons in support lib 28.0.0 (also reproducable in AndroidX v1.0.0)

I've tried to keep the changes very minimal from the tablayout (with viewpager) template in Android Studio 3.2.1. The first commit in the repo is just the template, the later commits are my changes.

In the code, the tab icon color is supposed to be set to a statelist which defines a yellow color for selected tabs and a 50% alpha yellow for unselected. I've tried it with both a vector and image asset, and finding the same issue in both.

The relevant code (for the vector icon) is here:

    TabLayout.Tab tab1 = tabLayout.getTabAt(0);
    VectorDrawableCompat iconVector = VectorDrawableCompat.create(getResources(), R.drawable.ic_tab_vector, getTheme());
    Drawable mutated1 = iconVector.mutate();
    ColorStateList stateList1 = ContextCompat.getColorStateList(this, R.color.tab_color_selector);
    DrawableCompat.setTintList(mutated1, stateList1);
    tab1.setIcon(mutated1);


This works as expected in 27.1.1:

![27.1.1 with tinted icons](/screenshots/27.1.1.png)

However, in 28.0.0 (or AndroidX1.0.0) The images just show as black (which are their base colors)

![28.0.0 with untinted icons](/screenshots/28.0.0.png)
