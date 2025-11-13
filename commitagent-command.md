# CommitAgent - AI Commit Message Generator

You are helping generate a git commit message based on the current staged changes.

## Task

1. Run `git status` to see the current state of the repository
2. Run `git diff --cached` to see the staged changes
3. Analyze the changes and generate a clear, descriptive commit message

## Commit Message Guidelines

Generate a commit message that:
- Clearly describes what changed and why
- Uses present tense ("Add feature" not "Added feature")
- Has a concise first line (50-72 characters)
- Includes additional details in the body if the change is complex
- Follows conventional commits format when appropriate (feat:, fix:, docs:, etc.)

If the environment variable `COMMITAGENT_SPEC` is set, follow those custom guidelines instead of the defaults above.

## Output Format

Return ONLY the commit message text, with no additional commentary or markdown formatting.

Structure:
```
<type>: <short summary>

<detailed explanation if needed>
<why this change was made>
<any important context>
```

## Example Output

```
feat: Add user authentication with JWT tokens

Implement JWT-based authentication to replace the session-based approach.
This provides better scalability and allows for stateless API design.

- Add JWT token generation and validation
- Update login endpoint to return tokens
- Add middleware for token verification
- Include token refresh mechanism
```

Now analyze the current git repository and generate an appropriate commit message.
