---
name: bragfast
description: Generate branded release announcement images and videos
---

# /bragfast — Generate Release Content

You are helping the user create branded release announcement images or videos using Bragfast.

## Step 1: Understand the Request

Ask the user: "What do you want to create? You can:"
- Paste a GitHub release URL
- Describe what you want (e.g., "Release images for v2.3.0 of my app")
- Say "video" if you want a release video

## Step 2: Gather Context

1. Call `bragfast_list_brands` to get available brands
2. Call `bragfast_list_templates` to get available templates
3. Present the options to the user:
   - **Brands:** List each brand by name. If none exist, ask for colors (background, text, primary as hex).
   - **Templates:** List each template by name. Recommend `standard-browser` as default.

Let the user pick a brand and template.

## Step 3: Compose Slides

Based on the user's input (release notes, GitHub URL, or description):

1. Extract the top 3-5 features or changes
2. For each slide, compose:
   - A short, punchy title (max ~40 chars)
   - A 1-2 line description
   - Map content to object IDs from the chosen template's config
3. Show the user the slide plan and ask for approval

**Important:** Look at the template config's `objects` array to find the correct object IDs for title, description, and image fields.

## Step 4: Generate

Based on what the user wants:

### For Images:
1. Call `bragfast_generate_release_images` with the composed slides
2. You'll get back a `cook_id`
3. Wait 5 seconds, then call `bragfast_get_render_status` with the cook_id
4. If still pending, wait another 5 seconds and check again (max 3 attempts)
5. When complete, show the image URLs to the user

### For Video:
1. Call `bragfast_generate_release_video` with the composed slides
2. You'll get back a `cook_id`
3. Wait 10 seconds, then call `bragfast_get_render_status`
4. Video renders take longer — check up to 6 times at 10-second intervals
5. When complete, show the video URL

## Step 5: Follow Up

After showing results:
- Show credits used and remaining
- Ask: "Want me to generate this in other formats? Or create a video version?"

## Error Handling

- If not authenticated: Tell the user to run `npx @bragfast/mcp-server login` or set `BRAGFAST_API_KEY`
- If insufficient credits: Show the credits needed and link to billing
- If render fails: Show the error and mention credits are auto-refunded

## Tips for Good Results

- Use the brand's colors and logo for consistent branding
- Keep slide titles short and impactful
- Use "browser" or "mobile" device frames for screenshots
- Square format works best for social media, landscape for blogs/newsletters
