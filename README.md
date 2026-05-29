# Personal Website | Muhammad Maaz

Personal portfolio site hosted on AWS S3 + CloudFront.

## Live URLs

- **Primary (HTTPS):** https://d13be0ebbetbkk.cloudfront.net
- **S3 origin (HTTP):** http://maazm-portfolio.s3-website-us-west-1.amazonaws.com

## Project Structure

```
personal-website/
├── index.html          # Main single-page site
├── style.css           # All styles
├── script.js           # Scroll animations, nav highlight
└── projects/
    └── ems/
        ├── index.html  # Power Grid EMS Simulator project page
        ├── system-architecture.svg
        └── simulation-loop.svg
```

The CAISO dashboard lives in a separate repo (`caiso-oasis-analysis`) and is deployed to Render, not here.

## AWS Infrastructure

| Resource | Name / ID |
|---|---|
| S3 bucket | `maazm-portfolio` (us-west-1) |
| CloudFront distribution | `E1ET99LYU58P7T` |
| IAM deploy user | `maaz-website-deployer` |
| AWS CLI profile | `maaz-website` |

## Deploying Changes

Make your edits, then run:

```bash
aws s3 sync . s3://maazm-portfolio/ \
  --exclude ".git/*" --exclude "README.md" \
  --profile maaz-website

aws cloudfront create-invalidation \
  --distribution-id E1ET99LYU58P7T \
  --paths "/*"
```

The CloudFront invalidation clears the cache so changes go live immediately. Without it, visitors may see the old version for up to 24 hours.

## Working on a New Machine

```bash
git clone https://github.com/Maaz679/personal-website.git
cd personal-website
```

Then configure the AWS CLI with the `maaz-website` IAM credentials:

```bash
aws configure --profile maaz-website
# Enter the Access Key ID and Secret from AWS IAM console
# Region: us-west-1
```

## Sections (in order)

1. **Hero** - Name, title, links
2. **Projects** - CAISO Analysis, EMS Simulator, AWS EDA Infra, C++ coursework
3. **Experience** - UmmahSoft, KiloWatts for Humanity, Masjid Muhajireen
4. **Skills** - Power Systems, Programming, Cloud & DevOps
5. **About** - Bio
6. **Contact** - Email, LinkedIn, GitHub
