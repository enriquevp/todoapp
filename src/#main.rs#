#[macro_use]
extern crate clap;
use clap::{Arg, App, SubCommand};

struct TodoItem {
    text: String,
    categories: Vec<String>
}

fn show_list(v: &Vec<TodoItem>) {
    for i in v.iter() {
        println!("- {}", i.text);
    }
}

fn show_list_by_category(v: &Vec<TodoItem>, cat: &String) {
    for i in v.iter() {
        for categ in &i.categories {
            if i.categories.is_empty() {
                println!("There are no items in that category.");
            } else {
                if categ == cat {
                    println!("- {}", i.text);
                }  
            }
        }
    }
}

fn main() {
    let matches = App::new("notetake")
        .version("0.1")
        .author("Enrique Villarreal <evillarreal@protonmail.com>")
        .about("Simple todolist in rust")
        .arg(Arg::with_name("item")
             .short("a")
             .long("add")
             .help("Adds a new item to the list")
             .takes_value(true))
        .arg(Arg::with_name("category")
             .short("c")
             .long("category")
             .help("Specifies the category the item belongs to")
             .takes_value(true)
             .multiple(true))
        .subcommand(SubCommand::with_name("show")
                    .about("Shows the list of items")
                    .arg(Arg::with_name("list_category")
                         .short("c")
                         .long("category")
                         .help("Shows all the items belonging to this category")
                         .takes_value(true)))
        .get_matches();

    let mut v: Vec<TodoItem> = vec![];
    if matches.is_present("item") {
        let user_item = value_t!(matches.value_of("item"), String).unwrap();
        let mut added_item: TodoItem = TodoItem{text : user_item.to_string(), categories : vec![]};

        if let Some(ref categories) = matches.values_of("category") {
            for in_categories in categories.iter() {
                added_item.categories.push(in_categories.to_string());
           } 
        }
        v.push(added_item);
    }

    if matches.is_present("show") {
        if matches.is_present("list_category") {
            let user_category = value_t!(matches.value_of("list_category"), String).unwrap();
            show_list_by_category(&v, &user_category.to_string());
        }
        if v.is_empty() {
            println!("The list is empty.");
        } else {
            show_list(&v);
        }
    }
}
