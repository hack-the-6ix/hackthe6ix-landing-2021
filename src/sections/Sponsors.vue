<template>
  <Section class="sponsors" id="sponsors" as="section">
    <SectionHeader
      align="center"
      bubble="Star"
      class="sponsors__heading"
      color="black"
    >
      Sponsors
    </SectionHeader>
    <div class="sponsors__groups">
      <ul
        v-for="[key, group] in Object.entries($static).filter(([k, g]) => k !== 'partner')"
        :class="[`sponsors__group--${key}`, 'sponsors__group']"
        :key="key"
      >
        <li v-for="(sponsor, index) in group.edges[0].node.logos" :key="index">
          <a :href="sponsor.description" target="_blank" class="sponsors__item">
            <img
              :class="[`sponsors__image--${key}`, 'sponsors__image', `sponsors__image--${sponsor.title}`]"
              :src="`https:${sponsor.file.url}`"
              :alt="sponsor.title"
            />
          </a>
        </li>
      </ul>
    </div>
    <SectionHeader
        align="center"
        bubble="Star"
        class="sponsors__heading sponsors__partner-heading"
        color="black"
    >
      Partners
    </SectionHeader>
    <div class="sponsors__groups">
      <ul
          :class="[`sponsors__group--partner`, 'sponsors__group']"
      >
        <li v-for="(sponsor, index) in $static.partner.edges[0].node.logos" :key="index">
          <a :href="sponsor.description" target="_blank" class="sponsors__item">
            <img
                :class="[`sponsors__image--partner`, 'sponsors__image']"
                :src="`https:${sponsor.file.url}`"
                :alt="sponsor.title"
            />
          </a>
        </li>
      </ul>
    </div>
  </Section>
</template>

<script>
import SectionHeader from '@/components/SectionHeader';
import Section from '@/components/Section';

export default {
  name: 'Sponsors',
  components: {
    SectionHeader,
    Section,
  },
};
</script>

<static-query>
{
  partner: allContentfulSponsorCategory(filter:{
    slug:{
      eq: "partner-2021"
    }
  }) {
    edges {
      node {
        logos {
          title
          description
          file {
            url
          }
        }
      }
    }
  }
  gold: allContentfulSponsorCategory(filter:{
    slug:{
      eq: "gold-2021"
    }
  }) {
    edges {
      node {
        logos {
          title
          description
          file {
            url
          }
        }
      }
    }
  }
  silver: allContentfulSponsorCategory(filter:{
    slug:{
      eq: "silver-2021"
    }
  }) {
    edges {
      node {
        logos {
          title
          description
          file {
            url
          }
        }
      }
    }
  }
  bronze: allContentfulSponsorCategory(filter:{
    slug:{
      eq: "bronze-2021"
    }
  }) {
    edges {
      node {
        logos {
          title
          description
          file {
            url
          }
        }
      }
    }
  }
}
</static-query>

<style lang="scss">
@use '@/styles/mixins';
@use '@/styles/colors';
@use '@/styles/units';

.sponsors {
  background-color: colors.css-color(white);
  padding-bottom: units.spacing(25);
  padding-top: units.spacing(25);

  &__bubble {
    margin-bottom: units.spacing(-2);
    margin-left: units.spacing(4);
  }

  &__heading {
    margin-bottom: units.spacing(8);
  }

  &__partner-heading {
    margin-top: units.spacing(13);
  }

  &__groups {
    margin-top: units.spacing(20);
  }

  &__group {
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    display: flex;
    padding: 0;
    margin: 0 0 units.spacing(14) 0;
  }

  &__item {
    display: flex;
  }

  &__image {
    @include mixins.transition(transform);
    margin: units.spacing(4) units.spacing(7) units.spacing(4) units.spacing(7);
    width: auto;
    height: 100vh;
    transform: scale(1);

    max-width: 90vw;

    &:hover {
      transform: scale(1.1);
    }

    &--partner {
      max-height: units.spacing(28);
      margin-top: -10px;
    }

    &--gold {
      max-height: units.spacing(28);
    }

    &--silver {
      max-height: units.spacing(15);
    }

    &--bronze {
      max-height: units.spacing(10);
      margin-left: units.spacing(4);
      margin-right: units.spacing(4);
    }

    /* Manual adjustments */
    &--rotman {
      max-height: units.spacing(15) !important;
    }
  }
}
</style>
