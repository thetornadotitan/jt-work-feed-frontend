<template>
  <div class="feed-item" v-bind:class="finalEntryType">
    <div class="header">
      <div class="source">
        Source:
        <br />
        {{feedItemData.Source}}
      </div>
      <div class="machine-name">
        Machine Name:
        <br />
        {{feedItemData.MachineName}}
      </div>
      <div class="user">
        User:
        <br />
        {{feedItemData.UserName}}
      </div>
      <div class="type">
        Type:
        <br />
        {{GetEntryTypeName(feedItemData.EntryType)}}
      </div>
      <div class="event-id">
        Event ID:
        <br />
        {{feedItemData.EventID}}
      </div>
    </div>
    <div class="body">
      <div class="date">{{GetLegibleTime(feedItemData.TimeGenerated)}}</div>
      <div class="message">{{feedItemData.Message}}</div>
      <div class="expanded" v-if="expanded">
        <button v-on:click="expanded=false" v-bind:class="finalEntryType">-Less Information-</button>
        <div>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</div>
      </div>
      <div class="collapsed" v-else>
        <button v-on:click="expanded=true" v-bind:class="finalEntryType">-More Information-</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'feed-item',
  props: ['feedItemData'],
  data: () => ({
    finalEntryType: '',
    expanded: false,
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
$errorcolor: #882424;
$warningcolor: #8a8824;
$informationColor: #004e97;
$successAuditcolor: #328332;
$failureauditcolor: $errorcolor;
$fontcolor: #ffffff;

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
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-column-gap: 15px;
    grid-row-gap: 30px;
    color: $fontcolor;
    text-shadow: 1px 1px #000000;
    padding: 0.25em;
  }
  .body {
    padding: 0.25em;
    color: $fontcolor;
    text-shadow: 1px 1px #000000;
    .date {
      margin-bottom: 0.75em;
    }
    .message {
      margin-bottom: 0.75em;
    }
  }
  .error {
    background: $errorcolor;
  }
  .warning {
    background: $warningcolor;
  }
  .information {
    background: $informationColor;
  }
  .successaudit {
    background: $successAuditcolor;
  }
  .failureaudit {
    background: $failureauditcolor;
  }
}

button {
  border: none;
  color: white;
  padding: 8px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  text-shadow: 1px 1px #000000;
  margin-bottom: 0.5em;
}
</style>
