<script lang="ts">
  import type { Career } from "../../types/career.type";
  import { CAREER_EMAIL } from "../../utils/constants";

  export let career: Career;

  const { title, intro, paragraphs, lists, textAfterTheLists, date } = career;
  const applicationEmail = `mailto:${CAREER_EMAIL}?subject=Application as ${title}`;

  const structuredData = {
    "@context": "https://schema.org/",
    "@type": "JobPosting",
    title: title,
    description: `
        <div>
            <p>${intro}</p>
            ${paragraphs
              .split("\n")
              .map((p) => `<p>${p}</p>`)
              .join(" ")}
            <div>
                ${lists
                  .map(
                    ({ title, items }) => `
                    <h4>${title}</h4>
                    <ul>
                        ${items.map((item) => `<li>${item}</li>`).join(" ")}
                    </ul>
                `
                  )
                  .join(" ")}
                <p>${textAfterTheLists}</p>
            </div>
        </div>
    `,
    datePosted: date,
    hiringOrganization: {
      "@type": "Organization",
      name: "Gitpod, Inc.",
      sameAs: "https://www.gitpod.io/",
      logo: "/images/gitpod-logo.svg",
      contactPoint: {
        "@type": "ContactPoint",
        url: "https://www.gitpod.io/contact/",
      },
    },
    // Location: Remote, anywhere on Earth.
    // Ref: https://developers.google.com/search/docs/data-types/job-posting#remote-jobs
    jobLocationType: "TELECOMMUTE",
    employmentType: "FULL_TIME",
    applicationContact: {
      "@type": "ContactPoint",
      email: applicationEmail,
    },
  };

  // Thanks to https://github.com/sveltejs/svelte/issues/5292#issuecomment-787743573
  const html = `<${""}script type="application/ld+json">${JSON.stringify(
    structuredData
  )}</${""}script>`;
</script>

{@html html}
