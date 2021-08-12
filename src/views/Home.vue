<template>
  <div class="qa-wrap">
    <div class="input-wrap">
      <label for="name">
        이름
      </label>
      <input type="text" class="name input" id="name" v-model="form.name">
      <label for="email">
        이메일
      </label>
      <input type="text" class="input" id="email"  v-model="form.email">
      <label for="text">
        문의내용
      </label>
      <textarea id="text" cols="30" rows="10" v-model="form.text"></textarea>
      <button class="submit-button" @click="submitQA">문의하기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      form: {
        name: '',
        email: '',
        text: '',
      },
    };
  },
  methods: {
    submitQA() {
      const blocks = {
        attachments: [
          {
            color: '#6b72f3',
            blocks: [
              {
                type: 'header',
                text: {
                  type: 'plain_text',
                  text: `🆘 ${this.form.name}님이 문의를 남겨주셨습니다!`,
                  emoji: true,
                },
              },

              {
                type: 'divider',
              },
              {
                type: 'section',
                fields: [
                  {
                    type: 'mrkdwn',
                    text: `*이름:*\n ${this.form.name}`,
                  },
                  {
                    type: 'mrkdwn',
                    text: `*문의 남긴 날짜:*\n ${new Date()}`,
                  },
                  {
                    type: 'mrkdwn',
                    text: `*이메일:*\n ${this.form.email}`,
                  },
                ],
              },
              {
                type: 'section',
                text: {
                  type: 'mrkdwn',
                  text: `*문의 내용:*\n ${this.form.text}`,
                },
              },
            ],
          },
        ],
      };
      this.axios.post('https://hooks.slack.com/services/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', JSON.stringify(blocks));
    },
  },
};
</script>

<style lang="scss" scoped>
.qa-wrap {
  height: 500px;
  border-radius: 13px;
  box-shadow: 0 0 10px 2px rgba(53, 56, 139, 0.1);
  background-color: #20233b;
  width: 500px;
  padding: 20px;
}

label {
  text-align: left;
  width: 100%;
  color: #FFF;
}
textarea{
  width: 100%;
  border-radius: 5px;
}

.input {
  border-radius: 5px;
  border: solid 1px #e7e7ed;
  width: 100%;
  height: 30px;
}

.submit-button{
  border-radius: 5px;
  background-color: #fff;
  width: 200px;
  color: #000;
  height: 50px;
  font-weight: bold;
}

.input-wrap {
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}
</style>
