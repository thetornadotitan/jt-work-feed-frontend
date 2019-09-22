<template>
  <div class="feed-item" v-bind:class="finalEntryType">
    <div class="header">
      <div class="source">{{feedItemData.Source}}</div>
      <div class="user">{{feedItemData.UserName}}</div>
      <div class="type">{{GetEntryTypeName(feedItemData.EntryType)}}</div>
      <div class="eventID">{{feedItemData.EventID}}</div>
    </div>
    <div class="body">
      <div class="date">{{GetLegibleTime(feedItemData.TimeGenerated)}}</div>
      <div class="message">{{feedItemData.Message}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'feed-item',
  props: ['feedItemData'],
  data: () => ({
    finalEntryType: '',
  }),
  methods: {
    GetEntryTypeName(entryType) {
      if (entryType === 1) {
        this.finalEntryType = 'error';
        return 'Error';
      }
      if (entryType === 2) {
        this.finalEntryType = 'warning';
        return 'Warning';
      }
      if (entryType === 4) {
        this.finalEntryType = 'information';
        return 'Information';
      }
      if (entryType === 8) {
        this.finalEntryType = 'successaudit';
        return 'SuccessAudit';
      }
      if (entryType === 18) {
        this.finalEntryType = 'failureaudit';
        return 'FailureAudit';
      }
      return 'none';
    },
    GetLegibleTime(unformattedTime) {
      const fixedString = unformattedTime.slice(
        unformattedTime.indexOf('(') + 1,
        unformattedTime.indexOf(')'),
      );
      return new Date(Number(fixedString));
    },
  },
};
</script>

<style lang="scss" scoped>
$errorcolor: #ff6666;
$warningcolor: #ffa600;
$informationColor: #6e9cff;
$successAuditcolor: #6fff6f;
$failureauditcolor: #ff6666;

.error {
  .header {
    background: $errorcolor;
  }
  border: 1px $errorcolor solid;
  border-radius: 5px;
  border-color: $errorcolor;
}

.warning {
  .header {
    background: $warningcolor;
  }
  border: 1px $warningcolor solid;
  border-radius: 5px;
  border-color: $warningcolor;
}

.information {
  .header {
    background: $informationColor;
  }
  border: 1px $informationColor solid;
  border-radius: 5px;
  border-color: $informationColor;
}

.successaudit {
  .header {
    background: $successAuditcolor;
  }
  border: 1px $successAuditcolor solid;
  border-radius: 5px;
  border-color: $successAuditcolor;
}

.failureaudit {
  .header {
    background: $failureauditcolor;
  }
  border: 1px $failureauditcolor solid;
  border-radius: 5px;
  border-color: $failureauditcolor;
}

.feed-item {
  margin: 1em;
  .header {
    display: grid;
    grid-template-columns: auto auto auto auto;
    color: black;
    padding: 0.25em;
  }
  .body {
    padding: 0.25em;
    .date {
      margin-bottom: 0.75em;
    }
  }
}
</style>
