---
title: ReactのMaterial-UIで、右揃えの要素を作るには
date: 2020-03-13 00:35:31
tags: 
- React
- javascript
---

こういう感じのやつです。特定の要素を右揃えにするのに少し苦労したのでメモっておきます。下の画像だとログインボタンがそれにあたります。

![image-20200313004013850](/images/react-spacer/image-20200313004013850.png)

結論から言うと`flexGrow: 1 `とした要素を挿入するだけです。VueのVuetifyでいうところの`v-spacer`コンポーネント的なやつですね。

```javascript
    <strong>タイトル</strong>
    <div style={{ flexGrow: 1 }}></div>
    <Button variant="contained" color="white">
      ログイン
    </Button>
```

　コード全体は以下の通りです。

```javascript
import React, { Component } from "react";
import PropTypes from "prop-types";
import { withStyles } from "@material-ui/core/styles";
import AppBar from "@material-ui/core/AppBar";
import Toolbar from "@material-ui/core/Toolbar";
import Button from "@material-ui/core/Button";
import IconButton from "@material-ui/core/IconButton";
import MenuIcon from "@material-ui/icons/Menu";

const styles = theme => ({
  root: {
    flexGrow: 1
  },
});

class Header extends Component {
  render() {
    const { classes } = this.props;
    return (
      <div className={classes.root}>
        <AppBar position="relative" color="primary">
          <Toolbar>
            <IconButton
              className={classes.menuButton}
              color="inherit"
              aria-label="Menu"
            >
              <MenuIcon />
            </IconButton>
            <strong>タイトル</strong>
            <div style={{ flexGrow: 1 }}></div>
            <Button variant="contained" color="white">
              ログイン
            </Button>
          </Toolbar>
        </AppBar>
      </div>
    );
  }
}

Header.propTypes = {
  classes: PropTypes.object.isRequired
};

export default withStyles(styles)(Header);
```

