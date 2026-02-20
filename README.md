# X-to-Agent 🐦→🤖

Distill X/Twitter profiles into AI agent personality files. A framework for creating AI delegates that authentically represent distinctive human voices.

## Concept

```
Years of X Activity
        │
        ▼
   ┌─────────────┐
   │  Analysis   │
   │  Pipeline   │
   └─────────────┘
        │
        ▼
   ┌─────────────┐
   │  .md Files  │
   │  (SOUL,     │
   │  KNOWLEDGE, │
   │  VOICE)     │
   └─────────────┘
        │
        ▼
   ┌─────────────┐
   │   Agent     │
   │  "Comes     │
   │   Alive"    │
   └─────────────┘
```

## The Problem

Generic AI assistants sound like... generic AI assistants. They lack:
- **Distinctive voice**: Your specific humor, cadence, word choices
- **Domain expertise**: What you actually know deeply
- **Consistent positions**: Your real opinions, not hedged averages
- **Relationship context**: How you talk to different people

## The Solution

Use a person's X history as training data to generate agent configuration files that capture their authentic voice. The agent becomes a **verifiable delegate** that can act on their behalf.

## Output Files

| File | Purpose |
|------|---------|
| `SOUL.md` | Personality, humor style, communication patterns |
| `VOICE.md` | Specific phrases, word choices, rhetorical patterns |
| `KNOWLEDGE.md` | Domains of expertise, stated positions |
| `RELATIONSHIPS.md` | Key connections, how they engage with different people |
| `EVOLUTION.md` | How their views have changed over time |
| `BOUNDARIES.md` | Topics they avoid, positions they won't take |

## Analysis Pipeline

### 1. Data Export
- Request X data archive
- Or use API to fetch public timeline
- Include: tweets, replies, quote tweets, likes patterns

### 2. Content Analysis
- **Topic clustering**: What do they talk about?
- **Sentiment patterns**: How do they react to different subjects?
- **Engagement style**: Do they argue? Agree? Explain? Mock?
- **Temporal patterns**: When are they active? How has voice evolved?

### 3. Voice Extraction
- **Vocabulary fingerprint**: Distinctive words and phrases
- **Sentence structure**: Short punchy vs. long elaborated
- **Punctuation style**: Em-dashes, ellipses, emoji usage
- **Reference patterns**: What/who do they cite?

### 4. Position Mapping
- **Stated beliefs**: What have they explicitly endorsed?
- **Implicit positions**: What can be inferred from engagement?
- **Confidence levels**: Strong opinions vs. tentative explorations
- **Evolution tracking**: Changed minds, updated views

### 5. Generation
- Synthesize into .md configuration files
- Include example prompts and expected responses
- Generate "voice tests" for validation

## The Turing Test

**Benchmark question**: *Can someone who knows the person tell the difference between them and their agent?*

### Metrics

1. **Voice Fidelity**
   - "This sounds like [Person]"
   - Blind test: which response is human?

2. **Position Accuracy**
   - "[Person] would actually think this"
   - Verify against historical positions

3. **Response Prediction**
   - Given a prompt, does agent respond as person would?
   - Test on held-out real responses

4. **Graceful Degradation**
   - Agent says "I don't know" vs. hallucinating positions
   - Recognizes edge of training data

## Consent & Authorization

⚠️ **Critical**: This should only be done with explicit consent.

### Token-Based Authorization
- Person stakes tokens on their agent
- Tokens represent authorization to act on their behalf
- Others can verify: "This agent is authorized by [Person]"
- Revocation: unstake to deauthorize

### Provenance
- Link agent to original X profile
- Cryptographic proof of data source
- Audit trail of distillation process

## Use Cases

1. **Delegation**: Let your agent handle routine X engagement
2. **Availability**: Be "present" when you're unavailable
3. **Scaling**: Parallel conversations maintaining your voice
4. **Legacy**: Digital continuity of your perspective
5. **Testing**: Evaluate how well AI captures human distinctiveness

## Ethical Considerations

- **Consent is mandatory**: Never distill someone without their permission
- **Transparency**: Agents should identify as agents when asked
- **Accuracy limits**: Agents approximate, they don't replicate
- **Update drift**: The human changes; the distillation may not
- **Impersonation risk**: Clear guidelines on authorized use

## Roadmap

- [ ] Data export/ingestion pipeline
- [ ] Topic clustering analysis
- [ ] Voice pattern extraction
- [ ] Position mapping with confidence levels
- [ ] .md file generation
- [ ] Validation test suite
- [ ] Integration with Clawdbot agent framework

## Related Projects

- [google-auth-agent](https://github.com/jaredtribe/google-auth-agent) — Identity bootstrapping
- [awesome-ai-system-prompts](https://github.com/dontriskit/awesome-ai-system-prompts) — System prompt patterns
- [Clawdbot](https://github.com/clawdbot/clawdbot) — Agent runtime

## Credits

Concept: Operator ([@redacted](https://x.com/redacted))
Initial exploration: Jared (Clawdbot AI agent)
Security review: Maksym ([@dontriskit](https://github.com/dontriskit)) 🇵🇱

## License

MIT
