# Technical Design

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     X-to-Agent Pipeline                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐ │
│  │  Ingest  │──▶│ Analyze  │──▶│ Generate │──▶│ Validate │ │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘ │
│       │              │              │              │        │
│       ▼              ▼              ▼              ▼        │
│  X Archive      Embeddings     .md Files      Test Suite   │
│  or API         + Clusters     + Prompts      + Metrics    │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## 1. Ingestion Layer

### Data Sources

**Option A: X Data Archive**
- User requests their data from X
- Provides complete history
- Includes DMs if authorized
- JSON format

**Option B: API Access**
- Limited to public tweets
- Rate limited
- Real-time updates possible
- Requires developer account

### Data Schema

```json
{
  "profile": {
    "username": "string",
    "display_name": "string",
    "bio": "string",
    "created_at": "datetime",
    "verified": "boolean"
  },
  "tweets": [
    {
      "id": "string",
      "text": "string",
      "created_at": "datetime",
      "type": "tweet|reply|quote|retweet",
      "in_reply_to": "string|null",
      "quoted_tweet_id": "string|null",
      "metrics": {
        "likes": "number",
        "retweets": "number",
        "replies": "number"
      }
    }
  ],
  "interactions": {
    "most_replied_to": ["username"],
    "most_quoted": ["username"],
    "conversation_threads": ["thread_id"]
  }
}
```

## 2. Analysis Layer

### Topic Clustering

1. Embed all tweets using sentence transformers
2. Cluster embeddings (HDBSCAN or similar)
3. Extract topic labels via LLM summarization
4. Track topic frequency and evolution over time

### Voice Pattern Extraction

**Lexical Analysis:**
- Vocabulary frequency
- Distinctive phrases (TF-IDF vs. baseline)
- Emoji/punctuation patterns
- Sentence length distribution

**Structural Analysis:**
- Thread vs. single tweet preference
- Quote tweet vs. reply patterns
- Time-of-day patterns
- Engagement response patterns

**Rhetorical Analysis:**
- Argument structures
- Evidence citation patterns
- Hedging language frequency
- Humor/irony markers

### Position Mapping

For each identified topic:
1. Extract all relevant tweets
2. Summarize stated positions
3. Identify confidence levels (strong, tentative, exploring)
4. Track evolution over time
5. Note contradictions or updates

## 3. Generation Layer

### SOUL.md Template

```markdown
# SOUL.md - Personality

## Core Identity
[Extracted from bio, pinned tweets, self-descriptions]

## Communication Style
[Derived from voice pattern analysis]

## Humor Patterns
[Examples of jokes, irony, wit from corpus]

## Engagement Philosophy
[How they interact: debate, support, inform, entertain]
```

### VOICE.md Template

```markdown
# VOICE.md - Distinctive Patterns

## Vocabulary
- Frequently used: [word list]
- Distinctive phrases: [phrase list]
- Avoided words: [patterns not used]

## Sentence Patterns
[Examples with annotations]

## Punctuation & Formatting
[Specific habits: em-dashes, caps, emoji]
```

### KNOWLEDGE.md Template

```markdown
# KNOWLEDGE.md - Domains & Positions

## Primary Domains
[Topics with highest engagement/expertise]

## Stated Positions
[Explicit views with citations]

## Inferred Positions
[Views implied by engagement patterns]

## Uncertainty Areas
[Topics where position is unclear or evolving]
```

## 4. Validation Layer

### Automated Tests

**Completion Tests:**
- Given first half of tweet, generate completion
- Compare to actual second half
- Measure semantic similarity

**Response Prediction:**
- Given tweet they replied to, predict their reply
- Compare to actual reply
- Score on voice + content

**Stance Detection:**
- Present topic, ask for position
- Compare to documented positions
- Check for hallucination

### Human Evaluation

**Blind Turing Test:**
1. Present evaluator with pairs: real tweet vs generated
2. Evaluator guesses which is real
3. Track accuracy across evaluators who know the person

**Quality Dimensions:**
- Voice authenticity (1-5)
- Position accuracy (1-5)
- Overall "sounds like them" (1-5)

## 5. Integration

### Clawdbot Integration

Generated .md files drop into Clawdbot workspace:
```
workspace/
├── SOUL.md        (personality)
├── VOICE.md       (distinctive patterns)
├── KNOWLEDGE.md   (positions)
├── AGENTS.md      (operational rules - separate)
└── IDENTITY.md    (boundaries - separate)
```

### Authorization Flow

1. User exports X data
2. Pipeline generates .md files
3. User reviews and edits
4. User deploys to agent
5. User stakes tokens to authorize
6. Agent operates as delegate

## Privacy & Security

- Raw X data processed locally or in trusted environment
- Generated files reviewed by user before deployment
- No retention of raw data after processing
- Consent verification at each step
