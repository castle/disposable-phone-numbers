# Disposable phone numbers

A curated list of the 1,000 most active disposable phone numbers, updated daily.

Maintained by [Castle's research team](https://castle.io/research/).

## Why this list exists

Disposable phone numbers are a key piece of infrastructure behind modern signup abuse.

Just like proxies help attackers distribute traffic and disposable email providers help them rotate identities cheaply, disposable phone number services help attackers bypass SMS verification systems at scale.

These services are commonly used for:

- Fake account creation
- Multi-accounting
- Promo abuse
- Referral abuse
- SMS verification bypass
- Spam operations

Over the years, we have observed the disposable phone number ecosystem becoming increasingly industrialized. Many providers now expose APIs specifically designed to automate SMS verification workflows across large numbers of accounts and platforms.

Despite how widely these services are used in abuse operations, high-quality disposable phone number datasets remain surprisingly difficult to find.

Most public lists are:
- Community-maintained
- Infrequently updated
- Aggregated from multiple public sources
- Extremely noisy
- Difficult to operationalize safely

We built this repository with a different philosophy.

- **Updated daily.** Fully automated pipeline, no dependency on community submissions.
- **Curated, not aggregated.** We do not import phone numbers from public repositories. Every number included in this dataset is independently verified and tied to a real disposable phone number service.
- **Observed in real abuse.** These phone numbers are actively used in fake signup campaigns, multi-accounting, and SMS verification abuse observed across Castle's network.
- **Small and focused.** Only 1,000 phone numbers. Smaller datasets are easier to operationalize safely and less likely to create unnecessary false positives.

If a phone number is included here, there is a strong reason for it.

## How we collect phone numbers

We continuously scrape disposable phone number provider websites to extract the phone numbers they expose publicly for SMS verification.

Many providers continuously rotate:
- Phone numbers
- Country coverage
- Telecom providers
- Virtual carrier infrastructure

Our collection pipeline tracks these changes continuously.

The list is ranked based on observed abuse prevalence across Castle's network, meaning the highest-signal phone numbers appear first.

## Repository contents

### Main list

```text
disposable-phone-numbers.txt
```

Plain text format:

```text
+15551234567
+447700900123
+33612345678
```

- One phone number per line
- E.164 format
- Sorted by observed abuse prevalence
- Most frequently abused numbers first

## Usage

Fetch the latest version directly from GitHub:

```bash
curl -sL https://raw.githubusercontent.com/castle/disposable-phone-numbers/master/disposable-phone-numbers.txt
```

The dataset is intentionally small enough to load entirely into memory.

### Example (Python)

```python
import urllib.request

URL = "https://raw.githubusercontent.com/castle/disposable-phone-numbers/master/disposable-phone-numbers.txt"

disposable_numbers = set(
    urllib.request.urlopen(URL)
    .read()
    .decode()
    .splitlines()
)

def is_disposable(phone_number: str) -> bool:
    return phone_number in disposable_numbers
```

### Example (JavaScript / Node.js)

```javascript
const response = await fetch(
  "https://raw.githubusercontent.com/castle/disposable-phone-numbers/master/disposable-phone-numbers.txt"
);

const text = await response.text();

const disposableNumbers = new Set(
  text.split("\n").map(n => n.trim()).filter(Boolean)
);

function isDisposable(phoneNumber) {
  return disposableNumbers.has(phoneNumber);
}
```

## What this list is not

### Not exhaustive

This repository only contains the top 1,000 disposable phone numbers currently observed in abuse activity.

Castle's internal dataset is significantly larger and continuously evolving.

### Not a blocking recommendation

How you use this data is up to you.

Different teams use disposable phone number signals differently:

- Hard blocking
- Risk scoring
- Step-up verification
- Rate limiting
- Manual review

Disposable phone number usage alone is not always malicious.

## Updates

The list is regenerated automatically every day and committed through an automated pipeline.

## License

MIT

## Links

- [Castle](https://castle.io/) - Account security and fraud prevention
- [Castle Research](https://castle.io/research/) - Threat research and technical articles
- [Castle Docs](https://docs.castle.io/) - API and product documentation