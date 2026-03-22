# Stardust CLI Reference

Auto-generated from the OpenAPI spec. Do not edit by hand.

## Authentication

All commands require `STARDUST_API_KEY` to be set:

```bash
export STARDUST_API_KEY=sj_your_key_here
```

## Commands

- [Artists](#artists)
- [Content](#content)
- [Events](#events)
- [Locations](#locations)
- [Map](#map)
- [Notes / Tags](#notestags)
- [Notes](#notes)
- [Notes / Collections](#notescollections)
- [Posts](#posts)
- [Recordings](#recordings)
- [Recordings / Collections](#recordingscollections)
- [Search](#search)
- [Songs](#songs)
- [Users](#users)
- [Other](#other)
- [User Links](#user-links)
- [Venues](#venues)

## Artists

### `create-artist`

**POST** `/artists`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | yes |  |
| `bio` | string | no |  |

**Example:**

```bash
stardust create-artist '{"bio": "Jazz pianist and composer", "name": "Thelonious Monk"}'
```

---

### `get-artist`

**GET** `/artists/{artist_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

### `get-artist-events`

**GET** `/artists/{artist_id}/events`

Get all events for an artist (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

### `request-membership`

**POST** `/artists/{artist_id}/members`

Request to join an artist. Creates a pending membership that an admin must approve.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

### `remove-own-membership`

**DELETE** `/artists/{artist_id}/members/me`

Remove your own membership from an artist.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

### `approve-membership`

**POST** `/artists/{artist_id}/members/{member_user_id}/approve`

Approve a pending membership request. Requires admin role.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |
| `member_user_id` | path | integer | yes |  |

---

### `reject-membership`

**POST** `/artists/{artist_id}/members/{member_user_id}/reject`

Reject a pending membership request. Requires admin role.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |
| `member_user_id` | path | integer | yes |  |

---

### `get-artist-notes`

**GET** `/artists/{artist_id}/notes`

Get all notes for an artist (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

### `get-artist-recordings`

**GET** `/artists/{artist_id}/recordings`

Get all recordings for an artist (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `artist_id` | path | integer | yes |  |

---

## Content

### `get-content-url`

**GET** `/content/{content_type}/{content_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `content_type` | path | `"recording"` \| `"note"` | yes |  |
| `content_id` | path | string | yes |  |

---

## Events

### `get-events-by-id`

**GET** `/events`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `create-event`

**POST** `/events`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | yes |  |
| `description` | string | no |  |
| `privacy` | `"private"` \| `"following"` \| `"public"` \| `"artist"` | no | `"private"` |
| `accepting_request_privacy` | `"private"` \| `"following"` \| `"public"` \| `"artist"` | no | `"private"` |
| `artist_ids` | integer[] | no |  |
| `venue_id` | integer | no |  |
| `started_at` | number | no |  |

**Example:**

```bash
stardust create-event '{"name": "Jazz Night", "privacy": "public", "venue_id": 5}'
```

---

### `get-event-by-uuid`

**GET** `/events/uuid/{uuid}`

Get event detail by UUID for deep linking.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `uuid` | path | string | yes |  |

---

### `post-event-users`

**GET** `/events/{code}/users`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `code` | path | string | yes |  |

---

### `get-event`

**GET** `/events/{event_id}`

Get event detail with recordings and notes.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

---

### `update-event`

**PUT** `/events/{event_id}`

Update an event. Only the creator can update.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | no |  |
| `description` | string | no |  |
| `privacy` | `"private"` \| `"following"` \| `"public"` \| `"artist"` | no |  |
| `accepting_request_privacy` | `"private"` \| `"following"` \| `"public"` \| `"artist"` | no |  |
| `artist_ids` | integer[] | no |  |
| `venue_id` | integer | no |  |
| `started_at` | number | no |  |

**Example:**

```bash
stardust update-event '{"name": "Jazz Night (updated)", "privacy": "public"}'
```

---

### `like-event`

**POST** `/events/{event_id}/like`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

---

### `set-rsvp-status`

**POST** `/events/{event_id}/rsvp`

Set or update the user's RSVP status for an event.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `status` | `"interested"` \| `"going"` \| `"not_responded"` \| `"performing"` \| `"not_going"` | yes |  |

---

### `get-set-list`

**GET** `/events/{event_id}/setlist`

Get the set list (ordered notes) for an event.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

---

### `add-to-set-list`

**POST** `/events/{event_id}/setlist`

Add a note or catalog song to the event's set list.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `note_id` | integer | no |  |
| `provider_track_id` | string | no |  |
| `provider` | string | no |  |
| `index` | integer | no |  |

---

### `reorder-set-list`

**PUT** `/events/{event_id}/setlist/reorder`

Reorder the set list items.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `note_ids` | integer[] | yes |  |

---

### `remove-from-set-list`

**DELETE** `/events/{event_id}/setlist/{note_id}`

Remove a note from the event's set list.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |
| `note_id` | path | integer | yes |  |

---

### `add-event-songs`

**GET** `/events/{event_id}/songs`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |
| `spotify_id` | query | string | no |  |

---

### `unlike-event`

**POST** `/events/{event_id}/unlike`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `event_id` | path | integer | yes |  |

---

## Locations

### `get-locations`

**GET** `/locations`

Get list of all locations for picker UI.

---

### `get-location`

**GET** `/locations/{location_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `location_id` | path | integer | yes |  |

---

## Map

### `get-map-events`

**GET** `/map/events`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `latitude` | query | number | yes |  |
| `longitude` | query | number | yes |  |
| `radius_km` | query | number | no | 50 |

---

## Notes / Tags

### `get-note-tags`

**GET** `/note-tags`

Get all note tags for the current user.

---

### `create-note-tag`

**POST** `/note-tags`

Create a new note tag.

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | yes |  |
| `emoji` | string | no |  |

---

### `delete-note-tag`

**DELETE** `/note-tags/{note_tag_id}`

Delete a note tag (soft delete).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_tag_id` | path | integer | yes |  |

---

### `update-note-tag`

**PUT** `/note-tags/{note_tag_id}`

Update an existing note tag.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_tag_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | no |  |
| `emoji` | string | no |  |

---

### `get-notes-by-note-tag`

**GET** `/notes/by-note-tag/{note_tag_id}`

Get all note IDs that have a specific note tag.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_tag_id` | path | integer | yes |  |

---

### `get-tags-for-note`

**GET** `/notes/{note_id}/note-tags`

Get all note tags for a specific note.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_id` | path | integer | yes |  |

---

### `set-tags-for-note`

**PUT** `/notes/{note_id}/note-tags`

Set the note tags for a note (replaces existing tags).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `note_tag_ids` | integer[] | yes |  |

---

### `remove-tag-from-note`

**DELETE** `/notes/{note_id}/note-tags/{note_tag_id}`

Remove a specific tag from a note (soft delete the junction record).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `note_id` | path | integer | yes |  |
| `note_tag_id` | path | integer | yes |  |

---

## Notes

### `get-notes-by-id`

**GET** `/notes`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `upload-note`

**POST** `/notes`

---

### `get-suggested-tips`

**POST** `/notes/suggested-tips`

Stream AI-powered playing tips for a cover song using Server-Sent Events.

Returns a stream of text chunks as they are generated, including:
- Song structure (verse, chorus, bridge, etc.)
- Chords for each section
- Notable elements (stops, tempo changes, play style)

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `song_name` | string | yes |  |
| `artist_name` | string | yes |  |

---

### `get-note-by-uuid`

**GET** `/notes/uuid/{uuid}`

Get note by UUID for deep linking.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `uuid` | path | string | yes |  |

---

## Notes / Collections

### `get-note-collections-by-id`

**GET** `/notes/collections`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `get-user-note-collections`

**GET** `/users/{created_by_id}/notes/collections`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `created_by_id` | path | integer | yes |  |
| `page` | query | integer | no | 1 |
| `per_page` | query | integer | no | 10 |

---

## Posts

### `create-post`

**POST** `/posts`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `description` | string | yes |  |
| `recording_id` | integer | no |  |
| `note_id` | integer | no |  |
| `event_id` | integer | no |  |

---

### `like-comment`

**POST** `/posts/comments/{comment_id}/like`

Like a comment.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `comment_id` | path | integer | yes |  |

---

### `unlike-comment`

**POST** `/posts/comments/{comment_id}/unlike`

Unlike a comment.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `comment_id` | path | integer | yes |  |

---

### `get-post-comments`

**GET** `/posts/{post_id}/comments`

Get all comments for a post, nested by replies.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `post_id` | path | integer | yes |  |

---

### `create-comment`

**POST** `/posts/{post_id}/comments`

Create a new comment on a post.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `post_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `body` | string | yes |  |
| `parent_id` | integer | no |  |

---

### `like-post`

**POST** `/posts/{post_id}/like`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `post_id` | path | integer | yes |  |

---

### `unlike-post`

**POST** `/posts/{post_id}/unlike`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `post_id` | path | integer | yes |  |

---

## Recordings

### `get-recordings-by-id`

**GET** `/recordings`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `upload-recording`

**POST** `/recordings`

---

### `get-recording-by-uuid`

**GET** `/recordings/uuid/{uuid}`

Get recording by UUID for deep linking.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `uuid` | path | string | yes |  |

---

### `get-recording`

**GET** `/recordings/{recording_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `recording_id` | path | integer | yes |  |

---

### `like-recording`

**POST** `/recordings/{recording_id}/like`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `recording_id` | path | integer | yes |  |

---

### `unlike-recording`

**POST** `/recordings/{recording_id}/unlike`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `recording_id` | path | integer | yes |  |

---

## Recordings / Collections

### `get-recording-collections-by-id`

**GET** `/recordings/collections`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `get-user-recording-collections`

**GET** `/users/{created_by_id}/recordings/collections`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `created_by_id` | path | integer | yes |  |
| `page` | query | integer | no | 1 |
| `per_page` | query | integer | no | 10 |

---

## Search

### `get-search`

**GET** `/search`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `term` | query | string | yes |  |
| `types` | query | `"user"` \| `"recording"` \| `"note"` \| `"event"` \| `"artist"` \| `"venue"` \| `"location"` \| `"catalog_song"`[] | yes |  |
| `page` | query | integer | no | 1 |
| `per_page` | query | integer | no | 50 |

**Example:**

```bash
stardust get-search "term=jazz&types=artist,event,venue&page=1&per_page=20"
```

---

## Songs

### `get-songs-by-id`

**GET** `/songs`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

## Users

### `get-users`

**GET** `/users`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `ids` | query | integer[] | yes |  |

---

### `get-notifications`

**GET** `/users/me/notifications`

Get pending membership requests for artists where this user is an admin.

---

### `get-preferences`

**GET** `/users/me/preferences`

---

### `update-preferences`

**PUT** `/users/me/preferences`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `music_provider` | string | yes |  |

---

### `clear-primary-artist`

**DELETE** `/users/me/primary-artist`

---

### `set-primary-artist`

**PUT** `/users/me/primary-artist`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `artist_id` | integer | yes |  |

---

### `get-user`

**GET** `/users/{user_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_id` | path | integer | yes |  |

---

### `get-user-events`

**GET** `/users/{user_id}/events`

Get all events for a user (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_id` | path | integer | yes |  |

---

### `get-user-notes`

**GET** `/users/{user_id}/notes`

Get all notes for a user (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_id` | path | integer | yes |  |

---

### `get-user-recordings`

**GET** `/users/{user_id}/recordings`

Get all recordings for a user (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_id` | path | integer | yes |  |

---

### `update-user`

**PUT** `/users/{user_to_change_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_to_change_id` | path | integer | yes |  |

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `first_name` | string | no |  |
| `last_name` | string | no |  |

---

### `get-profile-image-upload-url`

**POST** `/users/{user_to_change_id}/image/upload-url`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `user_to_change_id` | path | integer | yes |  |

---

## Other

### `list-api-keys`

**GET** `/users/me/api-keys`

---

### `create-api-key`

**POST** `/users/me/api-keys`

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | yes |  |

**Example:**

```bash
stardust create-api-key '{"name": "my-cli-key"}'
```

---

### `delete-api-key`

**DELETE** `/users/me/api-keys/{api_key_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `api_key_id` | path | integer | yes |  |

---

## User Links

### `add-user-link`

**POST** `/users/{logged_in_user_id}/user_links`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `logged_in_user_id` | path | integer | yes |  |
| `link_url` | query | string | yes |  |

---

### `delete-user-link`

**DELETE** `/users/{logged_in_user_id}/user_links/{link_to_delete_id}`

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `logged_in_user_id` | path | integer | yes |  |
| `link_to_delete_id` | path | integer | yes |  |

---

## Venues

### `create-venue`

**POST** `/venues`

Create a new venue.

**Body fields:**

| Field | Type | Required | Default |
|---|---|---|---|
| `name` | string | yes |  |
| `address` | string | no |  |
| `latitude` | number | no |  |
| `longitude` | number | no |  |

---

### `get-venue`

**GET** `/venues/{venue_id}`

Get venue details including upcoming events.

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `venue_id` | path | integer | yes |  |

---

### `get-venue-events`

**GET** `/venues/{venue_id}/events`

Get all events for a venue (used by 'Show More' button).

| Parameter | In | Type | Required | Default |
|---|---|---|---|---|
| `venue_id` | path | integer | yes |  |

---
