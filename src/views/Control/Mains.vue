<template>
  <div>
    <Breadcrumb :style="{ margin: '24px 0' }">
      <BreadcrumbItem>
        <Icon type="md-sync" :class="{ update }" @click="updatePage()" />
      </BreadcrumbItem>
      <!-- <BreadcrumbItem>Components</BreadcrumbItem> -->
      <BreadcrumbItem>控制台信息</BreadcrumbItem>
    </Breadcrumb>
    <Content
      :style="{ padding: '24px', minHeight: '280px', background: '#fff' }"
    >
      <div :class="{ center_box }">
        <Row :gutter="28">
          <Col span="12">
            <Card dis-hover>
              <p slot="title">待处理事项</p>
              <ul>
                <li v-for="item in items" :key="item.id">
                  <span>{{ item.name }}</span>
                  <router-link :to="{ name: 'messages' }">{{
                    item.state
                  }}</router-link>
                </li>
              </ul>
            </Card>
          </Col>
          <Col span="12">
            <Card dis-hover>
              <p slot="title">设计制作</p>
              <ul>
                <li v-for="make in makes" :key="make.id">
                  <span>{{ make.name }}</span>
                  <span>{{ make.content }}</span>
                </li>
              </ul>
            </Card>
          </Col>
        </Row>

        <Row :gutter="28">
          <Col span="12">
            <Card dis-hover>
              <p slot="title">账号信息</p>
              <ul>
                <li v-for="user in users" :key="user.id">
                  <span>{{ user.name }}</span>
                  <span>{{ user.content }}</span>
                </li>
              </ul>
            </Card>
          </Col>
          <Col span="12" :class="{ card_4 }">
            <Card dis-hover>
              <p slot="title">其他</p>
              <p :class="otherStyle">{{ other }}</p>
              <div>
                <Button type="success" @click="modal1 = true" :class="{ mail }"
                  >邮件反馈</Button
                >
                <Modal
                  v-model="modal1"
                  title="邮件反馈"
                  :styles="{ top: '0px', width: '700px' }"                 
                >
                  <div>
                    <p>邮件内容</p>
                    <Input
                      v-model="mailContent"
                      type="textarea"
                      :placeholder="value"
                      :rows="5"
                    />
                    <p>说明：给管理员写一封电子邮件，支持回车和换行</p>
                  </div>
                  <div slot="footer">
                    <Row type="flex" justify="center" :gutter="24">
                      <Col span="8">
                        <Button long @click="updatePage()">刷新</Button>
                      </Col>
                      <Col span="8">
                        <Button type="primary" long @click="handleSubmit()"
                          >提交</Button
                        >
                      </Col>
                      <Col span="8">
                        <Button long @click="modal1 = false">关闭</Button>
                      </Col>
                    </Row>
                  </div>               
                </Modal>
              </div>
            </Card>
          </Col>
        </Row>
      </div>
    </Content>
  </div>
</template>

<script>
export default {
  data() {
    return {
      center_box: "center_box",
      update: "update",
      card_4: "card_4",
      items: [
        { name: "在线留言：", state: "待审：0" },
        { name: "友情链接：", state: "待审：0" },
        { name: "用户注册：", state: "待审：0" },
      ],
      makes: [
        { name: "昵称：", content: "溪来鸿往" },
        { name: "邮箱：", content: "yiduweb@163.com" },
        { name: "QQ号：", content: "1908523972" },
        { name: "微信号：", content: "yoduhao918" },
      ],
      users: [
        { name: "用户名：", content: "demo" },
        { name: "姓名：", content: "鸿和" },
        { name: "登录时间：", content: "2022-5-17 21:19:26" },
      ],
      other: "如果您对本管理系统，有什么想法或建议，欢迎与我联系",
      otherStyle:"otherStyle",
      mail: "mail",
      span_state: "span_state",
      modal1: false,
      mailContent: "",
      value: "本邮件将发送到站长邮箱，请放心填写",
    };
  },
  methods: {
    handleSubmit() {
      if(this.mailContent == "") {
        this.$Message.warning("请输入邮件内容")
      }else{
      this.$Message.success("邮件发送成功，非常感谢您的反馈")
      this.modal1 = false
      }
    },
    updatePage() {
      this.$router.go(0);
    },
  },
};
</script>

<style lang="less" scoped>
.center_box ul {
  list-style-type: none;
}
.update {
  color: #337ab7;
  font-weight: bold;
  font-size: 22px;
  // padding-top: 18px;
  transform: rotate(-52deg);
  line-height: 12px;
}
.card_4 {
  margin-top: 11px;
}
.otherStyle {
  margin-bottom: 10px;
}
</style>