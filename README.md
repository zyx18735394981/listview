# listview
listview的优化_加载一种布局
   
  
     @Override
      public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder1 viewHolder1=null;
          if(convertView==null){
              //加载布局
              convertView=inflter.inflate(R.layout.list_item1, null);

              viewHolder1=new ViewHolder1();

              //找控件，把控件放入viewHolder1中
            viewHolder1.username= (EditText)convertView.findViewById(R.id.username);
            viewHolder1.age= (EditText)convertView.findViewById(R.id.age);
            viewHolder1.sex= (EditText)convertView.findViewById(R.id.sex);
            viewHolder1.icon=(ImageView)convertView.findViewById(R.id.icon);


              convertView.setTag(viewHolder1);
          }else{

              viewHolder1=(ViewHolder1)convertView.getTag();
          }

        //赋值
        viewHolder1.username.setText(list.get(position).getUsername());
        viewHolder1.age.setText(list.get(position).getAge());

        viewHolder1.sex.setText(list.get(position).getSex());
     



        return convertView;
    }



     //代理类找控件
       class ViewHolder1{
            EditText username,age,sex;

            ImageView icon;

    }
      }
 
 listview的优化_加载两种布局--getItemViewType() 和 getViewTypeCount()
 
      @Override
      public View getView(int position, View convertView, ViewGroup parent) {
          ViewHolder1 viewHolder1=null;
          ViewHolder2 viewHolder2=null;
          if(convertView==null){

              type= getItemViewType(position);

              switch (type){
                  case 0:
                      //加载布局
                      convertView=inflter.inflate(R.layout.list_item1, null);
                      viewHolder1=new ViewHolder1();
                      //找控件，把控件放入viewHolder1中
                      viewHolder1.username= (EditText)convertView.findViewById(R.id.username);
                      viewHolder1.age= (EditText)convertView.findViewById(R.id.age);
                      viewHolder1.sex= (EditText)convertView.findViewById(R.id.sex);
                     convertView.setTag(viewHolder1);
                      break;
                  case 1:
                      //加载布局
                      convertView=inflter.inflate(R.layout.list_item2, null);
                      viewHolder2=new ViewHolder2();
                      //找控件，把控件放入viewHolder1中
                      viewHolder2.username= (EditText)convertView.findViewById(R.id.username);
                      viewHolder2.age= (EditText)convertView.findViewById(R.id.age);
                      viewHolder2.sex= (EditText)convertView.findViewById(R.id.sex);
                     convertView.setTag(viewHolder2);
                      break;

              }

          }else{
                    switch (type){
                        case 0:
                            viewHolder1=(ViewHolder1)convertView.getTag();
                            break;
                        case 1:
                            viewHolder2=(ViewHolder2)convertView.getTag();

                    }

          }

        //赋值
        switch (type){
            case 0:
                viewHolder1.username.setText(list.get(position).getUsername());
                viewHolder1.age.setText(list.get(position).getAge()+"");
                viewHolder1.sex.setText(list.get(position).getSex());
                break;
            case 1:
                viewHolder2.username.setText(list.get(position).getUsername());
                viewHolder2.age.setText(list.get(position).getAge()+"");
                viewHolder2.sex.setText(list.get(position).getSex());
                break;

        }
        return convertView;
      }
    
        //       代理类找控件
               class ViewHolder1{
            EditText username,age,sex;

        }
             class ViewHolder2{
                 EditText username,age,sex;

             }

         //布局怎样区分
             @Override
             public int getItemViewType(int position) {
                 return position%2;
             }
         //几种布局
             @Override
             public int getViewTypeCount() {
                 return 2;
             }
             
             
 inflater的由来：
 
          //创建布局加载器
            inflter=(LayoutInflater)context.getSystemService(context.LAYOUT_INFLATER_SERVICE);
     
