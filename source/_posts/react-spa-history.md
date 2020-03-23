---
title: react-spa-history
date: 2020-03-24 00:54:54
tags:
 - React.js
 - react-router
---



# React+Material-UIで作るフォームのテンプレ的なやつ

Reactのコンポーネントは結構お約束というか決まり事みたいなのが多く、いちいち調べるのが面倒なのと雛形があれば使いまわせそうということでフォーム入力の形でテンプレ化してみました。公式通り (https://ja.reactjs.org/docs/forms.html) に入力項目ごとにstateのプロパティを設定して、name要素を定義して‥‥とやっているのですが、これかなり面倒な気がするのですがそういうものなのでしょうか‥‥入力内容のバリデーションは調べたんですがライブラリ的にしっくりくる感じのが少なく、結局`handleInputChange`内で逐一チェックするのが楽なような気がします。

```javascript
import React from "react";
import PropTypes from "prop-types";
import { withStyles } from "@material-ui/core/styles";
//materia-uiのコンポーネント
import Button from "@material-ui/core/Button";
import Grid from "@material-ui/core/Grid";
import TextField from "@material-ui/core/TextField";

//cssのスタイルを定義する
const styles = theme => ({
  root: {
    flexGrow: 1,
    overflow: "hidden",
    padding: theme.spacing(0, 3)
  },
  container: {
    margin: "auto"
  },
  textField: {
    width: 300
  }
});

function isNumber(numVal) {
  var pattern = /^[-]?([1-9]\d*|0)(\.\d+)?$/;
  return pattern.test(numVal);
}

class Content extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: "",
      age: 0
    };
    //これがないとハンドラ関数内でエラーが起きる
    this.handleInputChange = this.handleInputChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleInputChange(e) {
    //動的にプロパティ名を設定
    const name = e.target.name;
    this.setState({ [name]: e.target.value });
  }

  handleSubmit(e) {
    const name = this.state.name || "";
    const age = this.state.age || 0;
    const data = {
      name: name,
      age: age
    };
    //POST処理など
    //~~~~~~~~~~~
  }

  render() {
    const { classes } = this.props;
    return (
      <div className={classes.root}>
        <form>
      //グリッドレイアウトを設定するときは全体をcontainerグリッドで囲み、その中にitemグリッドを入れていく
          <Grid className={classes.container} container spacing={3}>
            <Grid item xs={12}>
              <h1>フォーム入力</h1>
            </Grid>
            <Grid item xs={12}>
              <TextField
                name="name"
                onChange={this.handleInputChange}
                className={classes.textField}
//簡単なバリデーション
                error={this.state.name.length < 10 ? false : true}
                label="name"
                placeholder="10字以内で入力"
                variant="outlined"
                autoComplete="off"
              />
            </Grid>
            <Grid item xs={12}>
              <TextField
                name="age"
                onChange={this.handleInputChange}
                className={classes.textField}
                error={isNumber(this.state.age ? false : true)}
                label="age"
                placeholder="半角英数字で入力"
                variant="outlined"
                autoComplete="off"
              />
            </Grid>
            <Grid item xs={12}>
              //ボタンはcontainedを設定しないと色が変わらないので注意
              <Button
                color="primary"
                variant="contained"
                onClick={this.handleSubmit}
              >
                送信
              </Button>
            </Grid>
          </Grid>
        </form>
      </div>
    );
  }
}

Content.propTypes = {
  classes: PropTypes.object.isRequired
};

export default withStyles(styles)(Content);

```

