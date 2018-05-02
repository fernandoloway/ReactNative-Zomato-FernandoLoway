// Project Zomato

import React, { Component } from 'react';
import { Image } from 'react-native';
import { Container, Header, Content, Card, CardItem, Thumbnail, Text, Button, Icon, Left, Body, Right, Item, Input } from 'native-base';
import axios from 'axios';

class App extends Component {


  constructor(){
    super();
    this.state= {restaurants:[], searchKey:''}
  }
  
  searchRestaurant(){
    var url='https://developers.zomato.com/api/v2.1/search?q='+this.state.searchKey;
    var config = {
      headers:{'user-key':'804b1ae84941c32b6e3d7d1d3e08b5b7'}
    };
    axios.get(url, config).then((rows)=> {
      // console.log(rows.data)
      this.setState({restaurants: rows.data.restaurants})
      console.log(this.state.restaurants)
    })
  }


  render() {

    const showList= this.state.restaurants.map((item, index)=>{
      var placeholderimg="data:image/png;base64,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"

      return (
        <Card key={index}>
          <CardItem>
            <Left>
              <Thumbnail square small source={{uri: item.restaurant.thumb ? item.restaurant.thumb : placeholderimg}} />
              <Body>
                <Text>{item.restaurant.name}</Text>
                <Text note>{item.restaurant.location.city}</Text>
              </Body>
            </Left>
            <Right>
              <Text>Rp {item.restaurant.average_cost_for_two/2}</Text>
            </Right>
          </CardItem>
          <CardItem cardBody>
            <Image source={{uri: item.restaurant.thumb ? item.restaurant.thumb : placeholderimg}} style={{height: 200, width: null, flex: 1}}/>
          </CardItem>
          <CardItem>
            <Left>
              <Button transparent>
                <Icon active name="ios-planet" />
              </Button>
              <Text>{item.restaurant.location.address}</Text>
            </Left>
          </CardItem>
        </Card>
      )
    })


    return (
      <Container>
         <Header searchBar rounded>
          <Item>
            <Icon name="ios-search" />
            <Input placeholder="Cari menu makanan ..." onChangeText={(inputUser) => {this.setState({searchKey:inputUser})}}
                value={this.state.searchKey} />
          </Item>
          {/* <Button transparent>
            <Text>Search</Text>
          </Button> */}
        </Header>
        <Button block onPress={()=>{this.searchRestaurant()}}>
          <Text>LIHAT DAFTAR RESTO</Text>
        </Button>
        <Content>
       
          {showList}

        </Content>
      </Container>
    );
  }
}


export default App;