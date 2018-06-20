<a href="https://github.com/storybooks/storybook/issues/2708">https://github.com/storybooks/storybook/issues/2708</a><div id="articleHeader"><h1>Addon-info doesn't show Proptypes and description</h1></div>
<p>Hi,<br />
I have problem with addon-info when I use my component as an external package. There is no problem when I copy the component source into my storybook project, but when call it from <strong>node module</strong> the <strong>PropType</strong> and <strong>description</strong> does not show</p>
<p><a href="https://user-images.githubusercontent.com/13084683/34774646-6332cfd6-f625-11e7-94f9-5b99a94334c3.png" target="_blank" class="readableLinkWithLargeImage"><div class="readableLargeImageContainer"><img src="https://user-images.githubusercontent.com/13084683/34774646-6332cfd6-f625-11e7-94f9-5b99a94334c3.png" alt="bug" /></div></a></p>
<p><a href="https://github.com/raadhoosh/fantastic-components/blob/master/src/Breadcrumb/Breadcrumb.js" target="_blank">My Component</a> source code :</p>
<div><pre>import React from 'react';
import PropTypes from 'prop-types';
import { Link } from 'react-router-dom';
import BreadcrumbStyled from './style/BreadcrumbStyled';
import OlStyled from './style/OlStyled';
import LiStyled from './style/LiStyled';

class Breadcrumb extends React.Component {
  render() {

    const {
      items, primary, secondary, info, success, danger, warning, rtl
    } = this.props;
    const elements = [];
    for (let i = 0; i &lt; items.length - 1; i += 1) {
      elements.push(items[i]);
    }
    const lastElement = items[items.length - 1];
    const themeProps = {
      primary, secondary, info, success, danger, warning, rtl
    };
    return (
      &lt;BreadcrumbStyled {...this.props}&gt;
        &lt;OlStyled {...themeProps}&gt;
          {elements.map((item, index) =&gt; {
            return (
              &lt;LiStyled
                key={index}
                {...themeProps}
              &gt;
                &lt;Link
                  to={item.path
                }&gt;
                  {item.name}
                &lt;/Link&gt;
              &lt;/LiStyled&gt;
            );
          })}
          &lt;LiStyled {...themeProps}&gt;{lastElement.name}&lt;/LiStyled&gt;
        &lt;/OlStyled&gt;
      &lt;/BreadcrumbStyled&gt;
    );
  }
}
Breadcrumb.propTypes = {
  /** array of objects */
  items: PropTypes.array.isRequired,
  /** rtl is true component show  in right side of the window, default is false (from left side). */
  rtl: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.primary color */
  primary: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.secondary color */
  secondary: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.info color */
  info: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.warning color  */
  warning: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.danger color  */
  danger: PropTypes.bool,
  /** Boolean indicating whether the component renders with Theme.success color */
  success: PropTypes.bool,
  /** The inline-styles for the root element. */
  style: PropTypes.object,
  /** The className for the root element. */
  className: PropTypes.string,
  /** The color renders with Theme.foreColor . */
  foreColor: PropTypes.string
};
Breadcrumb.defaultProps = {
  rtl: false,
  primary: false,
  secondary: false,
  info: false,
  warning: false,
  danger: false,
  success: false,
  style: {},
  className: '',
  foreColor: ''
};
export default Breadcrumb;</pre></div>
<p>I tried both <strong>compiling and installing from npm</strong> and <strong>linking to source code in github</strong>, there was no different.</p>
      